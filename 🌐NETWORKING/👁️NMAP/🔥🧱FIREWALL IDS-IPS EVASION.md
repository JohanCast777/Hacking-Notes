Intrusion Detection System(IDS)
Intrusion protection system(IPS) 


==SA only acknowledge== 
```shell-session
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace
```

==Create 5 randomly ips== ==-D RND:5==
```shell-session
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5
```

==Spoof the  source ip address== 
```shell-session
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```

==Choose a reliable source port==
```shell-session
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```

==Establish communication with one specific port ==
```shell-session
nc -nv 10.129.2.28 25
```
