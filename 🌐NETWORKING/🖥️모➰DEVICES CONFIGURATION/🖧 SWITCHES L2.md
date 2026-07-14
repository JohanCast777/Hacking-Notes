

- [✓] **Bacis Configuration**
    
- [✓] **VLANs & Trunking** (802.1Q)
    
- [✓] **Port Security** (MAC lockdown)
    
- [✓] **STP (Spanning tree)**
    
- [✓] **PortFast/BPDU Guard** (STP optimization)
    
- [✓] **EtherChannel** (LACP/Static)
    
- [✓] **VTP** (VLAN Sync)
    
- [✓] **CDP / LLDP**
    
- [✓] **L2 Security** (DHCP Snooping & Dynamic ARP Inspection)


## Bacis Configuration

```
enable
conf t
hostname [switch_name]
enable secret [password_name] || enable password ... - service password-encryption
banner motd [#Test#]#Command that creates a message to the device start
no ip domain lookup  #Don't search in DNS the wrong commands or any other text 
line concsle 0
logging synchronous      # this two last commands to create a new line after warniog
```

```
copy running-config startup-config
show run 
show ip interface brief
show interface status
```

## VLANs & Trunking (802.1Q)
(Virtual network that lives inside a physical switch)

Set access port (Pcs -> Switches)
```
enable
conf t
vlan 10
name Teachers
exit
int f0/1   
switchport mode access
switchport access vlan 10
no shut
end
wr
```

Set trunk port (Switches -> Switches || Switches -> Routers)
```
en
conf
int f0/3   
switchport mode trunk
switchport trunk native vlan 99 #Blocks attacks
switchport trunk allowed vlan 10,20  #For secure
exit
vtp mode transparent #Stay local(no delete disk)
vlan 999 #This is the black hole and it is to make some vlans unusables
name BLACKHOLE
exit
int range f0/6-23
switchport mode access
switchport access vlan 999
shutdown
end
wr
sh interface trunk
```

Make possible the comunication between different vlans (This is jut for switches that support L3 routing)
```
en 
conf
int vlan 10
ip add 192.168.10.1 255.255.255.0   #Represents the gatewa, this in every vlan
exit
ip routing
```


```
show vlan brief
```

## Port Security
(Isolates the port protected for unauthorized access)

```
conf t
int fa0/1
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky || switchport port-security mac-address 00d0.5809.2c42
end
```

```
show port-security interface fa0/1
show interface fa0/1 status
```

"We can confirm if that works connecting the interface to another computer and then connecting it back or the original one"

## STP (Spanning Tree)
(Protocol that ensures there is only one active path between any two network nodes)


Configure the core switch wit this commands
```
conf t
spanning-tree mode rapid-pvst
spanning-tree vlan 10 root primary   ! SW1 becomes root
end
```

```
show spanning-tree vlan 10
```

## PortFast + BPDY technology
(Skip the waiting states of Spanning Tree)

```
int fa0/1
 spanning-tree portfast
 spanning-tree bpduguard enable
end
```

The main problen of the STP is the time so this will be solved with "PortFast + BPDY technology"


![[Pasted image 20260214212909.png|400]]

## EtherChannel
(Allow the connection of 2 cables between 2 sitches)

This commands must to be set in both switches
```
en
conf
int range f0/1-2
channel-group 1 mode active
exit
int port-channel 1
switchport mode trunk
end 
show etherchannel summary
```

![[Pasted image 20260214184002.png]]


## VPT PROTOCOL
(Allows make changes that will be reflexted in all the topology)

First is important to understand the modes


|Mode|Creates/Deletes VLANs?|Uses VTP Updates?|Forwards VTP Updates?|VLAN Storage|Use Case|
|---|---|---|---|---|---|
|**Server**|✅ Yes|✅ Applies|✅ Yes|vlan.dat (flash)|**Master** switch – controls all VLANs in domain.[study-ccna+1](https://study-ccna.com/vtp-modes/)|
|**Client**|❌ No|✅ Applies|✅ Yes|vlan.dat (flash, from server)|Follows Server blindly – no local changes.[study-ccna+1](https://study-ccna.com/vtp-modes/)|
|**Transparent**|✅ Yes (local only)|❌ Ignores|✅ Yes (passes through)|running-config|**Safe relay** – your VLANs stay yours, forwards to others.[community.cisco+1](https://community.cisco.com/t5/switching/the-difference-between-vtp-server-and-transparent-mode-on/td-p/2490956)|
|**Off** (VTPv3 only)|✅ Yes (local)|❌ Ignores|❌ No|running-config|Total isolation – no VTP traffic at all.[study-ccna](https://study-ccna.com/vtp-modes/)​|


With this configuration the vlan 30 will be settlet automatically in the other switch
```
conf t
vtp mode server
vtp domain MYLAB
vtp version 2
vlan 30
 name LAB30
switchport mode trunk
end
```

```
conf t
vtp mode client
vtp domain MYLAB
vtp version 2
end
```





## CDP / LLDP

## L2 Security (DHCP Snooping & Dynamic ARP Inspection)

