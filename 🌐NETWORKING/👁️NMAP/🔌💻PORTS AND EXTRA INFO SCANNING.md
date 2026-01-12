==Port Status==

| `open`             | This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `closed`           | When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not. |
| `filtered`         | Nmap cannot correctly identify whether the scanned port is open or closed because either no response is returned from the target for the port or we get an error code from the target.                  |
| `unfiltered`       | This state of a port only occurs during the **TCP-ACK** scan and means that the port is accessible, but it cannot be determined whether it is open or closed.                                           |
| `open\|filtered`   | If we do not get a response for a specific port, `Nmap` will set it to that state. This indicates that a firewall or packet filter may protect the port.                                                |
| `closed\|filtered` | This state only occurs in the **IP ID idle** scans and indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.                                           |

==Most to least Stealthy==

| Command                                                                             | Technique (Description)                                                               | Typical Result                                                     | Stealth Level |
| ----------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------ | ------------- |
| sudo nmap 10.129.2.28 -sL -n --disable-arp-ping                                     | List Scan (-sL) No packets sent; just lists targets and does reverse DNS              | Target list with hostnames; no network activity                    | HIGHEST       |
| sudo nmap 10.129.2.28 -p 21 -sI zombiehost -Pn -n --packet-trace --disable-arp-ping | Idle/Zombie Scan (-sI) Uses zombie host IP; your real IP never appears in target logs | 21/tcp open ftp(ports shown open/closed; source masked)            | VERY HIGH     |
| sudo nmap 10.129.2.28 -p 21 -sN -Pn -n --packet-trace --disable-arp-ping            | TCP NULL Scan (-sN) Sends packets with no flags set; bypasses some firewalls          | `21/tcp open                                                       | filtered`     |
| sudo nmap 10.129.2.28 -p 21 -sF -Pn -n --packet-trace --disable-arp-ping            | TCP FIN Scan (-sF) Sends FIN packets only; evades basic firewalls                     | `21/tcp open                                                       | filtered`     |
| sudo nmap 10.129.2.28 -p 21 -sX -Pn -n --packet-trace --disable-arp-ping            | TCP Xmas Scan (-sX) Sets FIN, PSH, URG flags; "Christmas tree" scan                   | `21/tcp open                                                       | filtered`     |
| sudo nmap 10.129.2.28 -p 21 -sW -Pn -n --packet-trace --disable-arp-ping            | TCP Window Scan (-sW) Examines TCP window field in RST responses                      | 21/tcp openor21/tcp closed                                         | HIGH          |
| sudo nmap 10.129.2.28 -p 21 -sM -Pn -n --packet-trace --disable-arp-ping            | Maimon Scan (-sM) Sends FIN/ACK packets; named after Uriel Maimon                     | `21/tcp open                                                       | filtered`     |
| sudo nmap 10.129.2.28 -sn -n --disable-arp-ping                                     | Ping Scan (-sn) Host discovery only; sends ICMP/ARP to check if host is up            | Host is up (0.15s latency) No port information                     | MEDIUM-HIGH   |
| sudo nmap 10.129.2.28 -p 21 -sS -Pn -n --packet-trace --disable-arp-ping            | TCP SYN Scan (-sS) "Half-open" stealth scan; doesn't complete handshake               | 21/tcp open ftp                                                    | MEDIUM        |
| sudo nmap 10.129.2.28 -p 21 -sA -Pn -n --packet-trace --disable-arp-ping            | TCP ACK Scan (-sA) Maps firewall rules; sends ACK packets only                        | 21/tcp unfilteredor21/tcp filtered                                 | MEDIUM        |
| sudo nmap 10.129.2.28 -p 21 -sU -Pn -n --packet-trace --disable-arp-ping            | UDP Scan (-sU) Sends UDP packets; slow and often inconclusive                         | `21/udp open                                                       | filtered`     |
| sudo nmap 10.129.2.28 -p 21 -sO -Pn -n --packet-trace --disable-arp-ping            | IP Protocol Scan (-sO) Tests different IP protocols (TCP, ICMP, etc.)                 | Protocol responses (e.g.,1/tcp open icmp)                          | MEDIUM        |
| sudo nmap 10.129.2.28 -p 21 -sY -Pn -n --packet-trace --disable-arp-ping            | SCTP INIT Scan (-sY) Stream Control Transport Protocol INIT scan                      | 21/sctp openor21/sctp closed                                       | MEDIUM        |
| sudo nmap 10.129.2.28 -p 21 -sZ -Pn -n --packet-trace --disable-arp-ping            | SCTP COOKIE ECHO Scan (-sZ) Alternative SCTP scanning method                          | `21/sctp open                                                      | filtered`     |
| sudo nmap 10.129.2.28 -p 21 -sT -Pn -n --packet-trace --disable-arp-ping            | TCP Connect Scan (-sT) Full TCP handshake; easily logged and detected                 | 21/tcp open ftp                                                    | LOW           |
| sudo nmap 10.129.2.28 -p 21 -sV -Pn -n --packet-trace --disable-arp-ping            | Version Detection (-sV) Connects to grab service banners; more intrusive              | 21/tcp open ftp vsftpd 3.0.3                                       | VERY LOW      |
| sudo nmap 10.129.2.28 -sC -Pn -n --packet-trace --disable-arp-ping                  | Default Script Scan (-sC) Runs default NSE scripts for service enumeration            | Script output with detailed service info                           | VERY LOW      |
| sudo nmap 10.129.2.28 -O -Pn -n --packet-trace --disable-arp-ping                   | OS Detection (-O) Sends multiple probes to fingerprint OS; very noisy                 | OS details: Linux 4.4 – 5.3                                        | VERY LOW      |
| sudo nmap 10.129.2.28 -A -Pn -n --packet-trace --disable-arp-ping                   | Aggressive Scan (-A) Combines OS detection, version detection, scripts, traceroute    | 21/tcp open ftp vsftpd 3.0.3OS details, script output, traceroute… | LOWEST        |


| `10.129.2.28`        | Scans the specified target.                          |
| -------------------- | ---------------------------------------------------- |
| `-p 139`             | Scans only the specified port.                       |
| `--packet-trace`     | Shows all packets sent and received.                 |
| `-n`                 | Disables DNS resolution.                             |
| `--disable-arp-ping` | Disables ARP ping.                                   |
| `-Pn`                | Disables ICMP Echo requests.                         |
| <br>`--reason`       | Displays the reason a port is in a particular state. |
| --stats-every=5s<br> | Show the scanning status every 5 sec                 |
| -V                   | Real-time updates                                    |


==Check 10 most common ports==

```shell-session
sudo nmap 10.129.2.28 --top-ports=10
```

==Check an specific port== 

```shell-session
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
```

==Scan port aggressive== 

```shell-session
sudo nmap -sC -sV 10.129.252.92
```

