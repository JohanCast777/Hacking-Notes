
## SCAN HOSTS AVAILABLE IN A NET

==Scan Active devices in the Network==

```shell-session
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```

==Scan Active devices in the Network according to the doc "hosts.lst"==

```shell-session
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```

==If we want to scan some specific ips==

```shell-session
sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20| grep for | cut -d" " -f5

```

==Define range==

```shell-session
sudo nmap -sn -oA tnet 10.129.2.18-20| grep for | cut -d" " -f5
```

==Cat nmap file==

```shell-session
rep -oE '([0-9]{1,3}\.){3}[0-9]{1,3}' tnet.nmap | sort -u
```


## CHECK HOST STATUS

==Verify host is up first of all==

```shell-session
sudo nmap 10.129.2.18 -sn -oA host 
```

==Give us the reason why is up==

```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --reason
```

==Check ARP, ICMP also==

```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace 
```

==Disable ARP ping==

```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping 
```

==TTL types==

|Operating System|TTL Value|Notes|
|---|---|---|
|Linux/Unix|64|Most common modern Linux distributions|
|Windows|128|All modern Windows versions (NT 4.0+, 2000, XP, Vista, 7, 10, 11)|
|macOS|64|Modern macOS versions|
|FreeBSD|64|FreeBSD 5 and newer|
|Solaris/AIX|255|Traditional Unix systems|
|Cisco Routers|254-255|Network equipment|
|OpenBSD/NetBSD|255|BSD variants|
|Android|64|Mobile Linux-based OS|

==List of commands==[[Network_Enumeration_With_Nmap_Module_Cheat_Sheet.pdf]]
==Nmap Help==https://nmap.org/book/host-discovery-strategies.html

