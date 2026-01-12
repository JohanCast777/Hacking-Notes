
==OSI MODEL AND TPC MODEL==
![[Pasted image 20251027203458.png|500]]

![[Pasted image 20251112191806.png]]

![[Pasted image 20251112193756.png]]

| **Layer**        | **Function**                                                                                                                                                                                                                |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `7.Application`  | Among other things, this layer controls the input and output of data and provides the application functions.                                                                                                                |
| `6.Presentation` | The presentation layer's task is to transfer the system-dependent presentation of data into a form independent of the application.                                                                                          |
| `5.Session`      | The session layer controls the logical connection between two systems and prevents, for example, connection breakdowns or other problems.                                                                                   |
| `4.Transport`    | Layer 4 is used for end-to-end control of the transferred data. The Transport Layer can detect and avoid congestion situations and segment data streams.                                                                    |
| `3.Network`      | On the networking layer, connections are established in circuit-switched networks, and data packets are forwarded in packet-switched networks. Data is transmitted over the entire network from the sender to the receiver. |
| `2.Data Link`    | The central task of layer 2 is to enable reliable and error-free transmissions on the respective medium. For this purpose, the bitstreams from layer 1 are divided into blocks or frames.                                   |
| `1.Physical`     | The transmission techniques used are, for example, electrical signals, optical signals, or electromagnetic waves. Through layer 1, the transmission takes place on wired or wireless transmission lines.                    |

==TRANSMISION==


![[Pasted image 20251028204143.png|500]]

![[Pasted image 20251028204256.png|500]]

![[Pasted image 20251028204333.png|500]]

==MAC AND IP==

![[Pasted image 20251102190200.png|500]]
Linux command=ifconfig - cat /sys/class/net/*/address - ip link show
Windows command= get mac   -  ipconfig

==PORTS==

A port in networking is like a numbered doorway on a computer or server that helps direct different types of network traffic to the right program or service. Each port has a unique number, typically between 0 and 65535, which identifies it and corresponds to a specific function or protocol, such as port 80 for HTTP (web traffic) or port 22 for SSH (secure remote login).

![[Pasted image 20251102201955.png|500]]


![[Pasted image 20251102201031.png|500]]

- The **first type** (Well-Known Ports) are the most common and everyone knows them, like port 80 for websites or port 22 for secure logins.
    
- The **second type** (Registered Ports) are for specific companies or software that register their own ports, so they don’t conflict with others.
    
- The **third type** (Dynamic or Private Ports) are temporary ports used by your computer or apps like Filmora when they need to communicate over the network. You can assign or let the system pick these ports for your applications.


Work in the layer 4
Check active ports
windows= netstat -ano -p tcp
linux= netstat -antp

==BROWSING INTERNET EXAMPLE==
![[Pasted image 20251102213543.png|500]]


# DHCP

Automatically assigns IP addresses to devices on a network so they can communicate.
![[Pasted image 20251102215024.png | 500 ]]

# NAT

![[Pasted image 20251104224215.png|500]]

![[Pasted image 20251104225837.png|500]]

Main difference between ip private and public
![[Pasted image 20251104230056.png|500]]

# DNS

![[Pasted image 20251104231105.png|500]]

![[Pasted image 20251104231455.png|500]]


![[Pasted image 20251104233517.png|600]]


# INTERNET ARCHITECTURE 

==P2P==


![[Pasted image 20251105133616.png|500]]

==CLIENT SERVER==
![[Pasted image 20251105134128.png|500]]

|Architecture|Main Division|Scalability|Maintenance|Example|
|---|---|---|---|---|
|1-Tier|All-in-one|Poor|Hard|Standalone Access database|
|2-Tier|Client + Server|Moderate|Medium|Client app + direct DB connection|
|3-Tier|UI + Logic + Data|Good|Easy|Website + App server + DB server|
|N-Tier|Multiple layers|Excellent|Easiest|Enterprise apps, large web platforms|

==CLOUD ARCHITECTURE==

![[Pasted image 20251105162209.png|500]]

COMPARATIVE ALL THE TYPES OF ARCHITECTURES 

| `Architecture`  | `Centralized`                   | `Scalability`        | `Ease of Management`               | `Typical Use Cases`                |
| --------------- | ------------------------------- | -------------------- | ---------------------------------- | ---------------------------------- |
| `P2P`           | Decentralized (or partial)      | High (as peers grow) | Complex (no central control)       | File-sharing, blockchain           |
| `Client-Server` | Centralized                     | Moderate             | Easier (server-based)              | Websites, email services           |
| `Hybrid`        | Partially central               | Higher than C-S      | More complex management            | Messaging apps, video conferencing |
| `Cloud`         | Centralized in provider’s infra | High                 | Easier (outsourced)                | Cloud storage, SaaS, PaaS          |
| `SDN`           | Centralized control plane       | High (policy-driven) | Moderate (needs specialized tools) | Datacenters, large enterprises     |
# Wireless networks



![[Pasted image 20251105171648.png |500]]


![[Pasted image 20251105175413.png|500]]

# NETWORK SECURITY


==MOST IMPORTANT==

![[Pasted image 20251105193216.png|500]]


==FIREWALLS AND  IDS/IPS ==

![[Pasted image 20251105193958.png|700]]

Open source firewall for routers [pfsense](https://www.pfsense.org/) 

==FIREWALL TYPES==

| Firewall Type             | Main Function                                        | OSI Layer             | Pros                                    | Cons                          | Example Use                   |
| ------------------------- | ---------------------------------------------------- | --------------------- | --------------------------------------- | ----------------------------- | ----------------------------- |
| Packet Filtering          | Allows or blocks packets based on IP, port, protocol | Network (Layer 3)     | Fast, simple                            | No deep inspection            | Basic traffic control         |
| Stateful Inspection       | Tracks active connections and context of packets     | Transport (Layer 4)   | More secure than packet filtering       | Slightly slower               | Small or medium networks      |
| Application Layer (Proxy) | Filters traffic per application, uses proxies        | Application (Layer 7) | Deep inspection, hides internal network | Higher latency, complex setup | Web or email filtering        |
| Next-Generation (NGFW)    | Combines stateful + app control + IDS/IPS + user ID  | Multiple layers       | Very secure, full visibility            | Expensive, resource-heavy     | Enterprise security perimeter |



![[Pasted image 20251107204016 1.png|500]]


[Suricata](https://suricata.io/)

==HOW IT WORKS==

|**Techniques**|**Description**|
|---|---|
|`Signature-based detection`|Matches traffic against a database of known exploits.|
|`Anomaly-based detection`|Detects anything unusual compared to normal activity.|

==TYPES==

| Type      | Location      | Monitors           | Pros                                        | Cons                                                        | Example Use                  |
| --------- | ------------- | ------------------ | ------------------------------------------- | ----------------------------------------------------------- | ---------------------------- |
| HIDS/HIPS | Host device   | System files, logs | Detects insider/host-specific attacks       | Must install on every host, may impact performance          | Protect critical servers     |
| NIDS/NIPS | Network point | Network traffic    | Broad network visibility, centralized setup | May miss host-level attacks, can struggle with high traffic | Monitor traffic at perimeter |


# DATA FLOW EXAMPLES



![[Pasted image 20251107234242.png]]


![[Pasted image 20251107233752.png]]



==NETWORK TYPES==

![[Pasted image 20251112114946.png|500]]

**TYPES OF VPN**

![[Pasted image 20251112122641.png|500]]

![[Pasted image 20251126133317.png|500]]
NORMALLY USE ports `TCP/1723` and `UDP/500`
USE ENCAPSULATION PROTOCOL= [Encapsulating Security Payload](https://www.ibm.com/docs/en/i/7.4?topic=protocols-encapsulating-security-payload) (`ESP`)


==TOPOLOGIES==

Physic and logic distribution


![[Pasted image 20251112123453.png|500]]


![[Pasted image 20251112124443.png|500]]


==PROXY==

![[Pasted image 20251112132739.png]]

**Proxys aware**= Is when malware can bypass proxy
`WinSock` = Explorer, Edge, or Chrome
`libcurl` = FireFox (most secure)

**PROXY FORWARDING**

![[Pasted image 20251112183346.png|500]]

EXAMPLE
![[Pasted image 20251112170239.png|300]]

**REVERSE PROXY**

![[Pasted image 20251112185135.png|500]]

EXAMPLE
![[Pasted image 20251112185214.png|300]]

![[Pasted image 20251112185222.png|300]]

*(Non-) Transparent Proxy*



==IP ADDRESS==

![[Pasted image 20251114203718.png|500]]

![[Pasted image 20251114204419.png|500]]


![[Pasted image 20251202232733.png]]

![[Pasted image 20251202234722.png]]

| **Class** | **Network Address** | **First Address** | **Last Address** | **`Subnetmask`** | **CIDR**  | **Subnets** | **IPs**        |
| --------- | ------------------- | ----------------- | ---------------- | ---------------- | --------- | ----------- | -------------- |
| **A**     | 1.0.0.0             | 1.0.0.1           | 127.255.255.255  | `255.0.0.0`      | /8        | 127         | 16,777,214 + 2 |
| **B**     | 128.0.0.0           | 128.0.0.1         | 191.255.255.255  | `255.255.0.0`    | /16       | 16,384      | 65,534 + 2     |
| **C**     | 192.0.0.0           | 192.0.0.1         | 223.255.255.255  | `255.255.255.0`  | /24       | 2,097,152   | 254 + 2        |
| **D**     | 224.0.0.0           | 224.0.0.1         | 239.255.255.255  | `Multicast`      | Multicast | Multicast   | Multicast      |
| **E**     | 240.0.0.0           | 240.0.0.1         | 255.255.255.255  | `reserved`       | reserved  | reserved    | reserved       |


**BINARI NUMBERS**

![[Pasted image 20251114210748.png|500]]


**SUB-NETTING** 


- IPv4 Address: `192.168.12.160`
- Subnet Mask: `255.255.255.192`
- CIDR: `192.168.12.160/26`



| **Details of** | **1st Octet** | **2nd Octet** | **3rd Octet** | **4th Octet** | **Decimal**         |
| -------------- | ------------- | ------------- | ------------- | ------------- | ------------------- |
| IPv4           | `1100 0000`   | `1010 1000`   | `0000 1100`   | `10`10 0000   | 192.168.12.160`/26` |
| Subnet mask    | `1111 1111`   | `1111 1111`   | `1111 1111`   | `11`00 0000   | `255.255.255.192`   |
| Bits           | /8            | /16           | /24           | /32           |                     |

==NETWORK ADDRESS==set the ipv4 host bits in 0


| **Details of** | **1st Octet** | **2nd Octet** | **3rd Octet** | **4th Octet**     | **Decimal**             |
| -------------- | ------------- | ------------- | ------------- | ----------------- | ----------------------- |
| IPv4           | `1100 0000`   | `1010 1000`   | `0000 1100`   | `10`\|==00 0000== | 192.168.12.==128==`/26` |
| Subnet mask    | `1111 1111`   | `1111 1111`   | `1111 1111`   | `11`\|00 0000     | `255.255.255.192`       |
| Bits           | /8            | /16           | /24           | /32               |                         |

==BROADCAST ADDRESS== set the ipv4 host bits in 1

| **Details of** | **1st Octet** | **2nd Octet** | **3rd Octet** | **4th Octet**   | **Decimal**           |
| -------------- | ------------- | ------------- | ------------- | --------------- | --------------------- |
| IPv4           | 1100 0000     | 1010 1000     | 0000 1100     | 10\|==11 1111== | 192.168.12.==191==/26 |
| Subnet mask    | `1111 1111`   | `1111 1111`   | `1111 1111`   | `11\|00 0000    | 255.255.255.192       |
| Bits           | /8            | /16           | /24           | /32             |                       |


==TABLE FOR SUBNETTING==

| **Hosts**         | **IPv4**         |
| ----------------- | ---------------- |
| Network Address   | `192.168.12.128` |
| First Host        | `192.168.12.129` |
| Other Hosts       | `...`            |
| Last Host         | `192.168.12.190` |
| Broadcast Address | `192.168.12.191` |


==QUANTITY OF HOSTS USABLE===   

The 6 is from the host part
2^6-2= 62 

-------


==VLSM==

- Subnet: `192.168.12.128/26`
- Required Subnets: `4`

| **Details of** | **1st Octet** | **2nd Octet** | **3rd Octet** | **4th Octet**   | **Decimal**         |
| -------------- | ------------- | ------------- | ------------- | --------------- | ------------------- |
| IPv4           | 1100 0000     | 1010 1000     | 0000 1100     | 1000\| 0000     | 192.168.12.128`/28` |
| Subnet mask    | `1111 1111`   | `1111 1111`   | `1111 1111`   | ==1111==\| 0000 | `255.255.255.240`   |
| Bits           | /8            | /16           | /24           | /32             |                     |
Divide hosts 64/4= 16

==REPRESENTATION==

|**Subnet No.**|**Network Address**|**First Host**|**Last Host**|**Broadcast Address**|**CIDR**|
|---|---|---|---|---|---|
|1|`192.168.12.128`|192.168.12.129|192.168.12.142|`192.168.12.143`|192.168.12.128/28|
|2|`192.168.12.144`|192.168.12.145|192.168.12.158|`192.168.12.159`|192.168.12.144/28|
|3|`192.168.12.160`|192.168.12.161|192.168.12.174|`192.168.12.175`|192.168.12.160/28|
|4|`192.168.12.176`|192.168.12.177|192.168.12.190|`192.168.12.191`|192.168.12.176/28|


*BEST EXXPLANATION VLSM ANOTHER FOLDER*

# ==MAC==

![[Pasted image 20251120224431.png|500]]


![[Pasted image 20251120224002.png|500]]

![[Pasted image 20251120225043.png|500]]

# ==ARP==


![[Pasted image 20251120225654.png|500]]


**Example**

```shell-session
1   0.000000 10.129.12.100 -> 10.129.12.255 ARP 60  Who has 10.129.12.101?  Tell 10.129.12.100
2   0.000015 10.129.12.101 -> 10.129.12.100 ARP 60  10.129.12.101 is at AA:AA:AA:AA:AA:AA
```


![[Pasted image 20251120231410.png|500]]

![[Pasted image 20251120231300.png|500]]
**Main tools**

[Ettercap](https://github.com/Ettercap/ettercap) and  [Cain & Abel](https://github.com/xchwarze/Cain)

# ==IPV6==

![[Pasted image 20251124122258.png|500]]

![[Pasted image 20251124130210.png|500]]



| **Features**       | **IPv4**      | **IPv6**                     |
| ------------------ | ------------- | ---------------------------- |
| Bit length         | 32-bit        | 128 bit                      |
| OSI layer          | Network Layer | Network Layer                |
| Adressing range    | ~ 4.3 billion | ~ 340 undecillion            |
| Representation     | Decimal       | Hexadecimal                  |
| Prefix notation    | 10.10.10.0/24 | fe80::dd80:b1a9:6687:2d3b/64 |
| Dynamic addressing | DHCP          | SLAAC / DHCPv6               |
| IPsec              | Optional      | Mandatory                    |

[Hexadecimal system](https://www.shutterstock.com/es/image-vector/decimal-hexadecimal-binary-conversion-table-1990599341)



# ==THEORY WIRELESS NETWORKS== 

Radio frequency to communicate with each other 
![[Pasted image 20251124130451.png|500]] 
![[Pasted image 20251124130759.png|500]]

![[Pasted image 20251124132213.png|500]]

![[Pasted image 20251124134516.png|500]]




==WIFI CONNECTION==

![[Pasted image 20251124145504.png|500]]

![[Pasted image 20251124145739.png|500]]

# ==SECURE PROTOCOLS==


![[Pasted image 20251124160331.png|500]]

## ==ENCRIPTION PROTOCOLS==


==WEB==


![[Pasted image 20251124160757.png|500]]


[Cyclic Redundancy Check](https://en.wikipedia.org/wiki/Cyclic_redundancy_check) (`CRC`) =  plain text


==WPA==

![[Pasted image 20251124174305.png|500]]

![[Pasted image 20251124175828.png|500]]





## ==Authentication Protocols==


Provide a secure and standardized way of `verifying the identity` of users]



![[Pasted image 20251124182219.png|500]]


![[Pasted image 20251124182723.png|500]]

|**Protocol**|**Description**|
|---|---|
|`Kerberos`|Key Distribution Center (KDC) based authentication protocol that uses tickets in domain environments.|
|`SRP`|This is a password-based authentication protocol that uses cryptography to protect against eavesdropping and man-in-the-middle attacks.|
|`SSL`|A cryptographic protocol used for secure communication over a computer network.|
|`TLS`|TLS is a cryptographic protocol that provides communication security over the internet. It is the successor to SSL.|
|`OAuth`|An open standard for authorization that allows users to grant third-party access to their web resources without sharing their passwords.|
|`OpenID`|OpenID is a decentralized authentication protocol that allows users to use a single identity to sign in to multiple websites.|
|`SAML`|Security Assertion Markup Language is an XML-based standard for securely exchanging authentication and authorization data between parties.|
|`2FA`|An authentication method that uses a combination of two different factors to verify a user's identity.|
|`FIDO`|The Fast IDentity Online Alliance is a consortium of companies working to develop open standards for strong authentication.|
|`PKI`|PKI is a system for securely exchanging information based on the use of public and private keys for encryption and digital signatures.|
|`SSO`|An authentication method that allows a user to use a single set of credentials to access multiple applications.|
|`MFA`|MFA is an authentication method that uses multiple factors, such as something the user knows (a password), something the user has (a phone), or something the user is (biometric data), to verify their identity.|
|`PAP`|A simple authentication protocol that sends a user's password in clear text over the network.|
|`CHAP`|An authentication protocol that uses a three-way handshake to verify a user's identity.|
|`EAP`|A framework for supporting multiple authentication methods, allowing for the use of various technologies to verify a user's identity.|
|`SSH`|This is a network protocol for secure communication between a client and a server. We can use it for remote command-line access and remote command execution, as well as for secure file transfer. SSH uses encryption to protect against eavesdropping and other attacks and can also be used for authentication.|
|`HTTPS`|This is a secure version of the HTTP protocol used for communication on the internet. HTTPS uses SSL/TLS to encrypt communication and provide authentication, ensuring that third parties cannot intercept and read the transmitted data. It is widely used for secure communication over the internet, particularly for web browsing.|
|`LEAP`|LEAP is a wireless authentication protocol developed by Cisco. It uses EAP to provide mutual authentication between a wireless client and a server and uses the RC4 encryption algorithm to encrypt communication between the two. Unfortunately, LEAP is vulnerable to dictionary attacks and other security vulnerabilities and has been largely replaced by more secure protocols such as EAP-TLS and PEAP.|
|`PEAP`|PEAP on the other hand is a secure tunneling protocol used for wireless and wired networks. It is based on EAP and uses TLS to encrypt communication between a client and a server. PEAP uses a server-side certificate to authenticate the server and can also be used to authenticate the client using various methods, such as passwords, certificates, or biometric data. PEAP is widely used in enterprise networks for secure authentication.|

==HACK IT==

![[Pasted image 20251124185320.png|500]]



==Wireless Hardening==

![[Pasted image 20251124225827.png|500]]



# ==IPsec==

![[Pasted image 20251126175857.png|500]]

![[Pasted image 20251126181932.png|500]]
==IPsec ALLOW FIREWALL NEED==
![[Pasted image 20251126200342.png|500]]

==PPTP==

![[Pasted image 20251126201237.png|500]]

## ==VLANS==

![[Pasted image 20251126201501.png|500]]

![[Pasted image 20251126202340.png|500]]

1-4094

[CISO COMMANDS ](https://study-ccna.com/ios-basic-commands/)

![[Pasted image 20251126234027.png|700]]

![[Pasted image 20251127002515.png|500]]



![[Pasted image 20251127114809.png]]

![[Pasted image 20251128103958.png|500]]


[[🔢🏷️🔌VLANS]]


![[Pasted image 20251129003808.png]]

## ==KEY EXCHANGE ==

Used to exchange [cryptographic keys](https://www.cloudflare.com/learning/ssl/what-is-a-cryptographic-key/) between two parties securely.

![[Pasted image 20251130002635.png]]
![[Pasted image 20251130002839.png]]


![[Pasted image 20251130014926.png]]



## ==Cryptography==


![[Pasted image 20251203160322.png|700]]

