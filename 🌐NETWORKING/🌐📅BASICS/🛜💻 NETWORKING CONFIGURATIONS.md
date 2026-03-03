
==Check all the interfaces actives and inactive== 
```shell-session
ifconfig -a 
```

# NETSTATUS

| Option | Meaning   | What it shows                                                                                                  |
| ------ | --------- | -------------------------------------------------------------------------------------------------------------- |
| **-t** | TCP       | Show TCP connections (reliable, connection-based)                                                              |
| **-u** | UDP       | Show UDP connections (unreliable, connectionless)                                                              |
| **-l** | Listening | Only show ports that are **listening** for incoming connections                                                |
| **-n** | Numeric   | Show numeric IP addresses and port numbers instead of names (e.g., `127.0.0.1:80` instead of `localhost:http`) |
| **-p** | Program   | Show the **PID and program name** that owns each socket (e.g., `1234/apache2`)                                 |
| **-4** | IPv4      | Show only **IPv4** connections (not IPv6)                                                                      |
|        |           |                                                                                                                |

==Main example==
```shell
netstat -tulnp4
```

[PORT FORWARDING](https://youtu.be/2G1ueMDgwxw)

==Verify what is the path the ip is taking locally==
```shell-session
ip route get 10.129.233.197
```

==Verify what is the path the ip is taking in the network==
```shell-session
ping -c 1 -R 10.129.143.158
```

==Summary of the interfaces==

| **Interface Name**       | **Type**       | **Layer**     | **Typical Use**                                  | **Has Physical Hardware?** | **Example IP** | **Traffic Leaves Host?**                 |
| ------------------------ | -------------- | ------------- | ------------------------------------------------ | -------------------------- | -------------- | ---------------------------------------- |
| **lo**                   | Loopback       | L3 (IP)       | Internal self-communication                      | ❌ No                       | 127.0.0.1      | ❌ No                                     |
| **ens3 / eth0 / enpXsY** | Ethernet       | L2 + L3       | Wired network/internet access                    | ✅ Yes (or virtual)         | 209.50.61.235  | ✅ Yes                                    |
| **wlo1 / wlan0**         | Wireless       | L2 + L3       | Wi-Fi connectivity                               | ✅ Yes                      | 192.168.1.4    | ✅ Yes                                    |
| **tun0**                 | Tunnel         | L3 (IP)       | VPNs and encrypted tunnels                       | ❌ No                       | 10.10.14.21    | ✅ Indirectly (through another interface) |
| **tap0**                 | TAP            | L2 (Ethernet) | Virtualized environments, network emulation      | ❌ No                       | Varies         | ✅ Indirectly                             |
| **docker0**              | Bridge         | L2 + L3       | Communication between host and Docker containers | ❌ No                       | 172.17.0.1     | ❌ Usually stays internal                 |
| **virbr0**               | Virtual Bridge | L2 + L3       | Connects VMs to host or external network         | ❌ No                       | 192.168.122.1  | ✅ (via NAT)                              |


## GN3

==INSTALATION== 

[Instalation link ](https://www.gns3.com/software/download)

[Install Images routers](https://www.telectronika.com/descargas/cisco-imagenes-ios-para-gns3-dynamips-y-vm/)

[Cisco images]([https://community.cisco.com/t5/routing/images-for-gns3/td-p/3813389](https://ccnadesdecero.es/descargar-cisco-ios-gns3/))

==FIRST CONFIGURATION==

The router must be downloaded via iso file "images"

Types of images=

| Type                            | Features                                                         | Use Case                        | Example Images                                                                                                                                                                          |
| ------------------------------- | ---------------------------------------------------------------- | ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Beginner/Basic** (IP Base/K9) | Basic routing, VLANs, OSPF, EIGRP. Low RAM.                      | CCNA intro.                     | c3725-ipbasek9-mz.124-15.T14.bin [gns3](https://docs.gns3.com/docs/emulators/cisco-ios-images-for-dynamips/)​                                                                           |
| **Advanced** (adventerprisek9)  | + MPLS, BGP, IPSec VPN, QoS, full security (NAT, ACLs advanced). | CCNP, pentest labs, real‑world. | **c3725-adventerprisek9-mz.124-25d.bin** (your pick) [gns3]([https://docs.gns3.com/docs/emulators/cisco-ios-images-for-dynamips/](https://ccnadesdecero.es/descargar-cisco-ios-gns3/))​ |

Now follow this steps to insert the image and use the router(image)

Edit > Preferences > Dynamips > Iso Router > New > Local computer > Browse it > Skip warning > Select slot 0 > 




==COMMANDS==


## PCs

Se up ip in pc 
![[Pasted image 20260210002100.png]]

After select the net and right click to choose properties 

![[Pasted image 20260210002158.png]]
##### Putty Congifuration for Switches and Routers Management

Open device manaer and choose the console cable
![[Pasted image 20260210000419.png|500]]

Open Putty and shoose seria, then rename the serial line 
![[Pasted image 20260210000538.png]]

In Putty the ip configuration is like this
```
ip [dirección_ip] [máscara] [gateway]
show ip
save
sh ip int br # For Routers
sh ip route  # For Routers
```

## Switches L2

1. **VLANs/Trunking** (segmentation) ✓
    
2. **Port Security** (MAC lockdown) ✓
    
3. **STP/RSTP** (loop prevention) ✓
    
4. **EtherChannel** (redundancy/bandwidth) ✓
    
5. **VTP** (VLAN sync) ✓
    
6. **PortFast/BPDU Guard** (STP optimization) ✓

##### Main Congifuration
```
enable
conf t
hostname [switch_name]
enable secret [password_name]
show run #shows the commands setteled

```

##### Vlans
(Virtual network that lives inside a physical switch)

Set access port (Pcs -> Switches)
```
enable
conf t
vlan 10
name Profes
exit
int f0/1   
switchport mode access
switchport access vlan 10
no shut
end
wr
show vlan brief
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
ip add 192.168.10.1 255.255.255.0
exit
ip routing
```


##### Port Security
(Isolates the port protected for unauthorized access)

```
conf t
int fa0/1
 switchport mode access
 switchport access vlan 10
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky ||
	  switchport port-security mac-address 00d0.5809.2c42
end
show port-security interface fa0/1
show interface fa0/1 status
```

In case we want to delete some interfaces
```
conf t
int fa0/1
 no switchport port-security
 no switchport port-security mac-address 00d0.5809.2c42 ||
	 no switchport port-security mac-address sticky
 shut
 no shut
end
```

"We can confirm if that works connecting the interface to another computer and then connecting it back or the original one"

To activate the interface again is just with no shutdown
```
en
conf
int f0/1
suntdown
no suntdown
end 
```

##### STP (Spanning Tree)
(Protocol that ensures there is only one active path between any two network nodes)

The main problen of the STP is the time so this will be solved with "PortFast + BPDY technology"

![[Pasted image 20260214212909.png|400]]

Configure the core switch wit this commands
```
conf t
spanning-tree mode rapid-pvst
spanning-tree vlan 10 root primary   ! SW1 becomes root
end
show spanning-tree vlan 10
```


##### EtherChannel
(Allow the connection of 2 cables between 2 sitches)
![[Pasted image 20260214184002.png]]
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


##### VPT PROTOCOL
(Allows make changes that will be reflexted in all the topology)

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


##### PortFast + BPDY technology
(Skip the waiting states of Spanning Tree)

```
int fa0/1
 spanning-tree portfast
 spanning-tree bpduguard enable
end
```



## Routers

The main configuration is the same than the switch

Configuration ip
```
int g0/0 
ip address 192.168.1.1 255.255.255.0 
no shut
```

Configure ips with vlans
```
int g0/0
no shutdown
exit
int g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
no shutdown 
show run | inc encapsulation
```


##### DHCP

```
ip dhcp pool VLAN10
 network 192.168.10.0 255.255.255.0
 default‑router 192.168.10.1
 dns‑server 8.8.8.8 1.1.1.1
exit
ip dhcp excluded‑address 192.168.10.1
int g0/0
 ip address 192.168.10.1 255.255.255.0
 no shut
end
wr
show ip dhcp binding
show ip dhcp pool

```

##### Static Routing


![[Pasted image 20260218134850.png|600]]

First configure the network 10.0.0.0/30

Then configure the ip of every pc

Configure trunk in the switch

Create the vlans

Now use this commands to admit that we can sent ping to fartest router 

R1
```
conf t 
ip route 192.168.1.0 255.255.255.0 10.0.0.2 
ip route 192.168.0.0 255.255.255.0 10.0.0.2 
end
wr
```

R2
```
conf t 
ip route 192.168.1.0 255.255.255.0 10.0.0.1
ip route 192.168.0.0 255.255.255.0 10.0.0.1 
end
wr
```

##### Default static route

Keeping the same example picture, we can instead use this commands and it will work as well
```
conf t
ip route 0.0.0.0 0.0.0.0 10.0.0.1
end
wr
```

Note= We can use both together, and it is also recommendable

##### NAT
(Translates private ips "12.168..." to public ips "209.165...")

|Type|Function|How it works|Real use|
|---|---|---|---|
|**Static NAT**|**1 private = 1 fixed public**|Fixed mapping (192.168.1.10 ↔ 209.165.200.10)|**Servers** (web/mail – Internet initiates connection)|
|**Dynamic NAT**|**Private → public pool** (1:1 rotating)|Private gets temp public from pool (returns when done)|Medium offices (limited public IPs available)|
|**PAT (NAT Overload)**|**Many private → 1 public + ports**|192.168.1.10:80 → 209.165.200.1:50001|**Home/enterprise** (all PCs share 1 public IP)|
![[Pasted image 20260219190903.png]]
###### Static NAT


In the selected router we will make the configuration
```
conf t
ip nat inside source static 192.168.0.2 200.200.200.1
int g0/0
ip nat inside
exit
int s 0/1/0
ip nat outside
exit
sh ip nat translation
```

###### Dynamic NAT

```
conf t
access-list 1 permit 192.168.0.0 0.0.0.255
ip nat pool DYNAMIC 200.200.200.1 200.200.200.3 netmask 255.255.255.252
ip nat inside source list 1 pool DYNAMIC   ← NO "overload"
```

###### Overload Nat or PAT

```
conf t
access-list 1 permit 192.168.0.0 0.0.0.255
ip nat pool DYNAMIC 200.200.200.1 200.200.200.1 netmask 255.255.255.252
ip nat inside source list 1 pool DYNAMIC overload    ← KEY WORD!
end
```


##### ACL
(Traffic Filtering)

![[Pasted image 20260221183417.png|500]]

Thiis is the range 
![[Pasted image 20260221221637.png]]
###### Standart 
(BLocks only ip addresses)
![[Pasted image 20260221195421.png|400]]


![[Pasted image 20260221194557.png|700]]

```
conf t
access-list 10 deny 192.168.0.10      # Block PC .10
access-list 10 permit 192.168.0.0 0.0.0.255  # Allow all the network
int g0/0  # LAN interface
 ip access-group 10 in
show access-lists
no accesslist 
```


###### Extended 
(Blocks ips, protocols and ports)

![[Pasted image 20260221203705.png]]

```
access-list 101 deny tcp 192.168.0.0 0.0.0.255 any eq 80 
access-list 101 deny tcp 192.168.0.0 0.0.0.255 any eq 443 # HTTPS too 
access-list 101 permit ip any any # Allow everything else
interface g0/0
ip access-group 101 out # OUTBOUND = LAN→WAN
end
```

In order to test it use this

```
ping 200.200.200.0
telnet 200.200.200.0 80
```


Nother examples
(This example allos the communication of the 10.0.0.1:7777 to 54.4.4.4:80 )
```
access-list 101 permit tcp host 10.0.0.1 eq 7777 host 54.4.4.4 eq 80
```

```
access-list 101 permit ip host 10.0.0.11 host 54.4.4.4.7 #allow just the specific ips
```

```
access-list 101 permit ip 10.0.0.1 0.0.0.255 host 45.5.5.8
```

##### NAMED ACLS
(Same than access list, but the syntaxis is even easier)

```
ip access-list extended NAME
deny tcp 192.168.0.0 0.0.0.255 any eq 80 
deny tcp 192.168.0.0 0.0.0.255 any eq 443
remark Block HTTP/HTTPS from LAN   #Remember this are only commands
permit ip any any
```

##### RIP

|**Característica**|**RIP (v1 y v2)**|**OSPF (v2 y v3)**|
|---|---|---|
|**Tipo de Protocolo**|**Distance Vector** (Vector de Distancia)|**Link-State** (Estado de Enlace)|
|**Algoritmo**|Bellman-Ford|Dijkstra (SPF - Shortest Path First)|
|**Métrica**|**Conteo de saltos (Hops)**|**Costo** (basado en el ancho de banda)|
|**Límite de Tamaño**|Máximo **15 saltos** (16 es infinito)|Sin límite teórico (usa Áreas)|
|**Velocidad de Convergencia**|**Lenta** (depende de timers fijos)|**Muy Rápida** (reacciona a cambios)|
|**Actualizaciones**|Periódicas (cada 30 seg)|Basadas en eventos (LSA)|
|**Visión de la Red**|"Solo conoce a sus vecinos"|"Tiene un mapa completo de la red"|
|**Uso de CPU/RAM**|Muy bajo|Moderado a Alto|
|**Jerarquía**|Plana (todos los routers son iguales)|Jerárquica (Área 0, Áreas Secundarias)|
|**Distancia Administrativa**|**120**|**110**|
|**Estándar**|Abierto (RFC 1058/2453)|Abierto (RFC 2328)|

![[Pasted image 20260222170039.png|500]]
###### V1
```
conf
router rip 
network 192.168.1.0
network 10.0.0.0
show ip route rip   # Show
no router rip       # Delete
```

###### V2
```
conf t
router rip
 version 2              # ← RIPv2 (subnets + authentication)
 no auto-summary        # ← No classful auto-summarization
 passive-interface default # ← ALL interfaces passive no passive-interface   GigabitEthernet0/0 # ← EXCEPT LAN (send updates)
 network 192.168.1.0
 network 10.0.0.0
end
```



##### OSPF (DYNAMIC ROUTING)

Router1
```
conf t
router ospf 1
 router-id 1.1.1.1           # Unique ID per router "no mandatory"
 network 192.168.1.0 0.0.0.255 area 0  # LAN1
 network 200.1.1.0 0.0.0.3 area 0       # WAN link
end
show ip ospf neighbor
sh ip route ospf
sh ip ospf database
no router ospf 1

```

Router2
```
router ospf 1
 router-id 2.2.2.2
 network 192.168.2.0 0.0.0.255 area 0
 network 200.1.1.0 0.0.0.3 area 0
```

#### HSRP, VRRP, GLBP (FHRP)
(**All three provide redundant default gateways.** They solve the "single router failure = total outage" problem.)
##### HSRP (Hot Standby Router Protocol)

Use this Topology wit OSPF

![[Pasted image 20260226102859.png]]

Configure the virtual gateway in the pc (192.168.1.1)

Then follow the next commads for the router with the gateway


R0 (Active Router)
```
conf t
int g0/0
standby 1 ip 192.168.1.1
standby 1 priority 110
standby 1 preempt
end
```

R1 (Active Router)
```
conf t
int g0/0
standby 1 ip 192.168.1.1
standby 1 priority 100
standby 1 preempt
end
show standby brief
show ip interface brief | include 192.168.1
```

We can check if it works, sending pings from the pc to the last Router, additionally disconnecting the active and standby router.


##### VRRP (Virtual Router Redundancy Protocol)

Here is identical process, just we got to follow all the steps here (Remember Virtual or simulated GATEWAY)

Update first the gateway of the pc

Then follow these steps

R0 (Active Router)
```
conf t
int g0/0
vrrp 1 ip 192.168.1.1
vrrp 1 priority 110
vrrp 1 preempt
end
```

R1 (Active Router)
```
conf t
int g0/0
vrrp 1 ip 192.168.1.1
vrrp 1 priority 100
vrrp 1 preempt
end
no vrrp 1
show vrrp brief
show ip interface brief | include 192.168.1
```

Shutdown the interface where the cable was disconnected  !!IMPORTANT
##### GLBP
Again change tje pc gateway and shutdown the interface in case of test
```
conf t
int g0/0
glbp 1 ip 192.168.1.1
glbp 1 priority 100
glbp 1 preempt
end

no glbp 1

show glbp brief
show ip interface brief | include 192.168.1
```



