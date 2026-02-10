
==Check all the interfaces actives and inactive== 
```shell-session
ifconfig -a 
```

# NETSTATUS

|Option|Meaning|What it shows|
|---|---|---|
|**-t**|TCP|Show TCP connections (reliable, connection-based)|
|**-u**|UDP|Show UDP connections (unreliable, connectionless)|
|**-l**|Listening|Only show ports that are **listening** for incoming connections|
|**-n**|Numeric|Show numeric IP addresses and port numbers instead of names (e.g., `127.0.0.1:80` instead of `localhost:http`)|
|**-p**|Program|Show the **PID and program name** that owns each socket (e.g., `1234/apache2`)|
|**-4**|IPv4|Show only **IPv4** connections (not IPv6)|

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

[Cisco images](https://community.cisco.com/t5/routing/images-for-gns3/td-p/3813389)


==FIRST CONFIGURATION==

The router must be downloaded via iso file "images"

Types of images=

| Type                            | Features                                                         | Use Case                        | Example Images                                                                                                                    |
| ------------------------------- | ---------------------------------------------------------------- | ------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Beginner/Basic** (IP Base/K9) | Basic routing, VLANs, OSPF, EIGRP. Low RAM.                      | CCNA intro.                     | c3725-ipbasek9-mz.124-15.T14.bin [gns3](https://docs.gns3.com/docs/emulators/cisco-ios-images-for-dynamips/)​                     |
| **Advanced** (adventerprisek9)  | + MPLS, BGP, IPSec VPN, QoS, full security (NAT, ACLs advanced). | CCNP, pentest labs, real‑world. | **c3725-adventerprisek9-mz.124-25d.bin** (your pick) [gns3](https://docs.gns3.com/docs/emulators/cisco-ios-images-for-dynamips/)​ |

Now follow this steps to insert the image and use the router(image)

Edit > Preferences > Dynamips > Iso Router > New > Local computer > Browse it > Skip warning > Select slot 0 > 




==COMMANDS==


### PCs

Check the pc information
```
show ip
```

Set ip 
```
ip 192.168.1.10 255.255.255.0 192.168.1.1
```

Check the connectivity with devices
```
ping 192.168.1.20
```

Save all the conf
```
save
```

Show the arp 
```
show arp
```

Reloads saved conf
```
load
```

### Switches

##### Main Congifuration
```
enable
conf t
hostname [switch_name]
enable secret [password_name]
show run #shows the commands setteled

```

##### Vlans

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
vtp mode transparent #Stay local(no delete disk)
exit
vlan 999 #This is the black hole and it is to make some vlans unusables
name BLACKHOLE
exit
int range f0/6-23
switchport mode access
switchport access vlan 999
shutdown
end
wr
```


