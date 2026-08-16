
# 🌐 CCNA Module 2: Switching, Routing, and Wireless Essentials (SRWE)

Welcome to the **CCNA Module 2 (SRWE)** study guide and lab reference! This repository covers intermediate network operations including VLAN segmentation, Spanning Tree Protocol (STP), EtherChannel link aggregation, Inter-VLAN routing, and Wireless LAN (WLAN) fundamentals for the Cisco CCNA (200-301) exam.

---

## 📌 Table of Contents
- [1. VLANs & Trunking Configuration (802.1Q)](#1-vlans--trunking-configuration-8021q)
- [2. Spanning Tree Protocol (STP) & EtherChannel](#2-spanning-tree-protocol-stp--etherchannel)
- [3. Inter-VLAN Routing (Router-on-a-Stick & SVI)](#3-inter-vlan-routing-router-on-a-stick--svi)
- [4. Dynamic Host Configuration Protocol (DHCPv4)](#4-dynamic-host-configuration-protocol-dhcpv4)
- [5. First Hop Redundancy Protocols (FHRP)](#5-first-hop-redundancy-protocols-fhrp)
- [6. Switch Security & Port Security](#6-switch-security--port-security)
- [7. Verification & Troubleshooting Commands](#7-verification--troubleshooting-commands)

---

## 1. VLANs & Trunking Configuration (802.1Q)

VLANs partition a physical switch into distinct broadcast domains, while 802.1Q trunks allow multiple VLANs to traverse a single link.

### VLAN Creation & Port Assignment
```cisco
! Create VLANs and assign descriptive names
vlan 10
 name Sales
exit

vlan 20
 name Engineering
exit

! Assign access interface to a specific VLAN
interface FastEthernet 0/1
 description Access Port for Sales PC
 switchport mode access
 switchport access vlan 10
 no shutdown
 exit

```

### Trunking Configuration

```cisco
interface GigabitEthernet 0/1
 description 802.1Q Trunk to Distribution Switch
 switchport mode trunk
 switchport trunk native vlan 99
 switchport trunk allowed vlan 10,20,99
 no shutdown
 exit

```

---

## 2. Spanning Tree Protocol (STP) & EtherChannel

Preventing Layer 2 loops while bundling multiple physical interfaces into a logical link (LACP/PAgP).

### Rapid PVST+ & PortFast Configuration

```cisco
! Enable Rapid Spanning Tree Protocol
spanning-tree mode rapid-pvst

! Set Primary/Secondary Root Bridge priority for VLAN 10
spanning-tree vlan 10 root primary

! Enable PortFast and BPDU Guard on end-user access ports
interface FastEthernet 0/1
 spanning-tree portfast
 spanning-tree bpduguard enable
 exit

```

### EtherChannel Configuration (LACP - Standards-based)

```cisco
! Configure physical interfaces
interface range GigabitEthernet 0/1 - 2
 description LACP Trunk Bundle
 switchport mode trunk
 channel-group 1 mode active
 exit

! Configure logical Port-Channel interface
interface Port-channel 1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,99
 exit

```

---

## 3. Inter-VLAN Routing (Router-on-a-Stick & SVI)

Enabling Layer 3 communication between isolated VLANs.

### Option A: Router-on-a-Stick (RoAS)

```cisco
! Ensure physical interface is active with no IP assigned
interface GigabitEthernet 0/0/0
 no shutdown
 exit

! Subinterface for VLAN 10
interface GigabitEthernet 0/0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 exit

! Subinterface for VLAN 20
interface GigabitEthernet 0/0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 exit

```

### Option B: Layer 3 Switch (Switch Virtual Interfaces)

```cisco
! Enable IP Routing on Layer 3 Switch
ip routing

! Create SVIs for L3 Gateway functionality
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
 exit

interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
 exit

```

---

## 4. Dynamic Host Configuration Protocol (DHCPv4)

Configuring a Cisco router as a DHCP server or relay agent.

### Router as DHCPv4 Server

```cisco
! Exclude static IPs (gateways, servers, printers)
ip dhcp excluded-address 192.168.10.1 192.168.10.10

! Configure DHCP Pool
ip dhcp pool VLAN10_POOL
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8
 domain-name lab.local
 lease 2
 exit

```

### DHCP Relay Agent (ip helper-address)

```cisco
! Configured on the router interface facing clients when DHCP server is remote
interface GigabitEthernet 0/0/0.10
 ip helper-address 10.0.0.100
 exit

```

---

## 5. First Hop Redundancy Protocols (FHRP)

High availability gateway redundancy using HSRP (Hot Standby Router Protocol).

```cisco
! Router 1 (Active) Configuration
interface GigabitEthernet 0/0/0.10
 standby version 2
 standby 10 ip 192.168.10.254
 standby 10 priority 110
 standby 10 preempt
 exit

```

---

## 6. Switch Security & Port Security

Mitigating common Layer 2 attacks (MAC Flooding, DHCP Spoofing).

### Port Security Baseline

```cisco
interface FastEthernet 0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
 exit

```

### DHCP Snooping (Anti-Spoofing)

```cisco
ip dhcp snooping
ip dhcp snooping vlan 10,20

! Trust uplink ports facing legitimate DHCP servers
interface GigabitEthernet 0/1
 ip dhcp snooping trust
 exit

```

---

## 7. Verification & Troubleshooting Commands

Essential audit commands for Layer 2 and Layer 3 switching operations.

```cisco
! VLAN & Trunking Audit
show vlan brief
show interfaces trunk

! Spanning Tree & EtherChannel Audit
show spanning-tree summary
show etherchannel summary

! DHCP Audit
show ip dhcp binding
show ip dhcp pool

! L2 MAC Table Audit
show mac address-table

```

---

## 📂 Related Labs

Check out the Packet Tracer `.pkt` files inside the [`/labs`](https://www.google.com/search?q=./labs) directory to test these configurations interactively!

```

***

<ElicitationsGroup message="How would you like to build out this module next?">
  <Elicitation label="Create a Router-on-a-Stick Packet Tracer lab guide" query="Write a step-by-step Packet Tracer lab guide for Router-on-a-Stick Inter-VLAN routing to include in Module 2."/>
  <Elicitation label="Draft the Module 3 (ENSA) Cheatsheet next" query="Let's move on to the CCNA Module 3 (ENSA) cheatsheet and generate its README.md."/>
</ElicitationsGroup>

```