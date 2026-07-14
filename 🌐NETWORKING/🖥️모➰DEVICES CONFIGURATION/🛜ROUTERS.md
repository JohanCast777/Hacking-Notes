

- [✓] **Bacis Configuration**
    
- [✓] **Router on a Stick (Allow vlans comunication)**
    
- [✓]  **Static & Default Routing**
    
- [✓]  **RIP (Routing Information Protocol)**
    
- [✓]  **OSPF (DYNAMIC ROUTING)**
    
- [✓]  **NAT (Network address Translation)**
    
- [✓]  **ACLs**


## Bacis Configuration

```

enable
conf t
hostname R1
no ip domain-lookup
service password-encryption
enable secret [password_name] || enable password ... - service password-encryption
banner motd [#Test#]#Command that creates a message to the device start
line concsle 0
logging synchronous      # this two last commands to create a new line after 
int g0/0 
ip address 192.168.1.1 255.255.255.0 
no shut
```

```
show ip route
show ip interface brief
show run | section line
show ssh
```


## Router on a Stick (Allow vlans comunication)

```
int g0/0
no shutdown
exit
int g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
no shutdown
```

```
show run | inc encapsulation
```

## Static & Default Routing

##### Static Routing
![[Pasted image 20260304114746.png]]


R1
```
ip route 192.168.10.0 255.255.255.0 10.0.0.2
```

R0
```
ip route 192.168.10.0 255.255.255.0 10.0.0.1
```

##### Default static route

R1
```
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

R0

```
ip route 0.0.0.0 0.0.0.0 10.0.0.1
```


```
sh ip route
sh ip route static
sh ip route connected
sh ip route 192.168.10.10  # Reach specific ip
```


We can combine them, but we have to see what fit more.

## RIP (Routing Information Protocol)
(Routing protocol used by routers to exchange routing information and determine the best path)

| Feature                     | RIP (v1 & v2)             | OSPF (v2 & v3)                    |
| --------------------------- | ------------------------- | --------------------------------- |
| **Protocol Type**           | Distance Vector           | Link-State                        |
| **Algorithm**               | Bellman-Ford              | Dijkstra (SPF)                    |
| **Metric**                  | Hop Count                 | Cost (bandwidth-based)            |
| **Size Limit**              | Max 15 hops (16=infinite) | No theoretical limit (uses Areas) |
| **Convergence Speed**       | Slow (fixed timers)       | Very Fast (event-triggered)       |
| **Updates**                 | Periodic (every 30s)      | Event-based (LSA)                 |
| **Network View**            | "Only knows neighbors"    | "Complete network map"            |
| **CPU/RAM Usage**           | Very Low                  | Moderate to High                  |
| **Hierarchy**               | Flat (all routers equal)  | Hierarchical (Area 0, Areas)      |
| **Administrative Distance** | 120                       | 110                               |
| **Standard**                | Open (RFC 1058/2453)      | Open (RFC 2328)                   |

![[Pasted image 20260222170039.png|500]]



###### Version 1
```
conf
router rip 
network 192.168.1.0
network 10.0.0.0
```

###### Version 2
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

```
show ip route rip   
```

## OSPF (DYNAMIC ROUTING)

R1
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

R2
```
router ospf 1
 router-id 2.2.2.2
 network 192.168.2.0 0.0.0.255 area 0
 network 200.1.1.0 0.0.0.3 area 0
```


## NAT (Network address Translation)
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


## ACLs
(Traffic Filtering)

Thiis is the range of every type of ACL
![[Pasted image 20260221221637.png]]

###### Standart 
(BLocks only ip addresses)

![[Pasted image 20260221194557.png|700]]

![[Pasted image 20260221195421.png|400]]

```
conf t
access-list 10 deny 192.168.0.10      # Block PC .10
access-list 10 permit 192.168.0.0 0.0.0.255  # Allow all the network
int g0/0  
 ip access-group 10 in         # This deny access for all the LAN
||
int s0/0
	ip access-group 10 out     # This deny access for wan, or internet
```

###### Extended 
(Block ips, protocols and ports)

![[Pasted image 20260221203705.png]]


access-list 101 deny 



```
show access-lists
```


