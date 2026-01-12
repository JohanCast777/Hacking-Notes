
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


