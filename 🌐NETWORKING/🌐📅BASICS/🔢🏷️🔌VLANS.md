
## ==SET VLAN WITH IEEE 802.1Q ==


LINUX

==Check the 8012q avaliability ==
```shell-session
sudo modprobe 8021q
```

==Check if running correctly==
```shell-session
lsmod | grep 8021
```

==Check the interface name==
```shell-session
ip a
```

==Set the vlan in a new interface==
```shell-session
sudo ip link add link eth0 name eth0.20 type vlan id 20
```

==Commands for interfaces==
ip link show | grep wlo1.20
sudo ip link set dev wlo1.20 down
sudo ip link delete wlo1.20
sudo ip link add link wlo1 name wlo1.20 type vlan id 20
sudo ip link set dev wlo1.20 up

==Set ip new interface for the vlan==
```shell-session
sudo ip addr add 192.168.1.1/24 dev eth0.20
```

==Start VLAN==
```shell-session
sudo ip link set up eth0.20
```

WINDOWS

==Set a vlan==

![[Pasted image 20251128225501.png]]

![[Pasted image 20251128225537.png]]

![[Pasted image 20251128225551.png]]


==ANALYZING VLAN TAGGED TRFFIC==
## ==ANALYSING VLAN TAGGED TRAFFIC==

![[Pasted image 20251128225923.png]]



## ==VLAN HOPPING ==

![[Pasted image 20251128231546.png]]
MAIN TOOL [Yersinia](https://linux.die.net/man/8/yersinia)

![[Pasted image 20251129001710.png|500]]



![[Pasted image 20251129002215.png]]


[Scapy](https://scapy.readthedocs.io/en/latest/usage.html#vlan-hopping)
![[Pasted image 20251129002314.png]]

