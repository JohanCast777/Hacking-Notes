  
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


## Routers

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




##### ACL


![[Pasted image 20260221183417.png|500]]








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



