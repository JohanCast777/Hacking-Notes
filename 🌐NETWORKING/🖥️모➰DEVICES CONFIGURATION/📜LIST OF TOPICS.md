

## 🛠️ 1. The Layer 2 Switch (Access Layer)

_The "Gatekeeper." It handles physical cables and identifies devices by MAC addresses._

- [✓] **VLANs & Trunking** (802.1Q)
    
- [✓] **STP / RSTP** (Loop prevention)
    
- [✓] **EtherChannel** (LACP/Static)
    
- [✓] **Port Security** (MAC lockdown)
    
- [✓] **VTP** (VLAN Sync)
    
- [ ] **CDP / LLDP** (Neighbor discovery: `show cdp neighbors`)
    
- [ ] **L2 Security** (DHCP Snooping & Dynamic ARP Inspection)
    

---

## ⚡ 2. The Layer 3 Switch (Multilayer Switch)

_The "Hybrid." It does everything a L2 switch does, but can also route traffic between VLANs._

- [✓] **Inter-VLAN Routing (SVIs)** (The `int vlan 10` commands)
    
- [ ] **IP Routing Activation**: Crucial! Routers have this on by default; L3 switches need the command `ip routing`.
    
- [ ] **Routed Ports**: Turning a switch port into a "router port" using `no switchport`.
    
- [ ] **Layer 3 EtherChannel**: Assigning an IP address to a Port-Channel interface.
    

---

## 🛣️ 3. The Router (The Edge/Gateway)

_The "Navigator." It connects different networks and speaks to the Internet._

- [✓] **IPv4 Addressing / Subnetting**
    
- [✓] **Static & Default Routing**
    
- [✓] **Router-on-a-Stick** (Sub-interfaces: `int g0/0.10`)
    
- [✓] **OSPFv2** (Dynamic Routing)
    
- [✓] **NAT / PAT** (Inside/Outside translation)
    
- [✓] **ACLs** (Standard, Extended, Named)
    
- [✓] **DHCP Server** (Pools and Exclusions)
    
- [✓] **FHRP (HSRP/VRRP/GLBP)** (Gateway Redundancy)
    
- [ ] **IPv6 Routing** (Configuring `ipv6 unicast-routing` and OSPFv3)
    

---

## 📡 4. Wireless: WLC & Access Points

_The "Airwaves." Configuration here is mostly done via a Web Browser (GUI)._

- [ ] **WLC (Wireless LAN Controller)**: Creating WLANs, SSIDs, and Security (WPA2/WPA3).
    
- [ ] **LAP (Lightweight Access Point)**: Understanding how it joins the WLC via **CAPWAP** tunnels.
    
- [ ] **WLC Management**: Configuring the "Management Interface" vs "Data Interface."
    

---

## 🛡️ 5. Next-Gen Firewall (NGFW) & IPS

_The "Bodyguard." While often a separate device, you need to know its role compared to a Router._

- [ ] **Stateless vs. Stateful Inspection**: Understanding why firewalls are "smarter" than ACLs.
    
- [ ] **IPS (Intrusion Prevention System)**: Detecting and dropping malicious signatures in real-time.
    
- [ ] **Security Zones**: Defining "Inside" (Trusted), "Outside" (Internet), and "DMZ" (Public Servers).
    

---

## 💻 6. The Management PC (The Modern Brain)

_The "Architect." In the new CCNA, this is where Automation and SDN happen._

- [ ] **Cisco DNA Center**: The central "Dashboard" for managing the whole network.
    
- [ ] **SD-Access / SD-WAN**: Concepts of fabric, underlay (physical), and overlay (virtual).
    
- [ ] **Automation Tools**: Knowing the difference between **Ansible** (Push/Python), **Puppet**, and **Chef** (Pull/Ruby).
    
- [ ] **JSON Data**: Being able to read the code format used for network automation.