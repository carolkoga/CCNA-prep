
---

# 🌐 CCNA Module 3: Enterprise Networking, Security, and Automation (ENSA)

Welcome to the **CCNA Module 3 (ENSA)** study guide and lab reference! This repository covers large-scale enterprise network concepts, single-area OSPFv2, WAN technologies, Network Security (ACLs, NAT), Network Management (NTP, SNMP, Syslog), and Software-Defined Networking / Automation for the Cisco CCNA (200-301) exam.

---

## 📌 Table of Contents

* [1. Single-Area OSPFv2 Configuration](https://www.google.com/search?q=%231-single-area-ospfv2-configuration)
* [2. Network Security & Access Control Lists (ACLs)](https://www.google.com/search?q=%232-network-security--access-control-lists-acls)
* [3. Network Address Translation (NAT)](https://www.google.com/search?q=%233-network-address-translation-nat)
* [4. WAN Concepts & Site-to-Site VPNs](https://www.google.com/search?q=%234-wan-concepts--site-to-site-vpns)
* [5. Network Management (NTP, Syslog, SNMP)](https://www.google.com/search?q=%235-network-management-ntp-syslog-snmp)
* [6. Network Automation, SDN & REST APIs](https://www.google.com/search?q=%236-network-automation-sdn--rest-apis)
* [7. Verification & Troubleshooting Commands](https://www.google.com/search?q=%237-verification--troubleshooting-commands)

---

## 1. Single-Area OSPFv2 Configuration

OSPF is an open-standard Link-State routing protocol used in enterprise networks.

### Basic OSPFv2 Single-Area (Area 0)

```cisco
! Enable OSPF process with Process ID 10
router ospf 10
 router-id 1.1.1.1
 network 192.168.10.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
 auto-cost reference-bandwidth 1000
 passive-interface GigabitEthernet 0/0/0
 exit

```

### Interface-Level OSPF & Default Route Propagation

```cisco
! Interface-level OSPF configuration (preferred modern syntax)
interface GigabitEthernet 0/0/1
 ip ospf 10 area 0
 ip ospf cost 10
 exit

! Propagate default route (0.0.0.0/0) to OSPF neighbors from Edge Router
router ospf 10
 default-information originate
 exit

```

---

## 2. Network Security & Access Control Lists (ACLs)

ACLs filter traffic based on source, destination, protocol, and port numbers.

### Standard IPv4 ACL (Filter based on Source IP only - place near destination)

```cisco
! Allow specific host and subnet, deny rest
ip access-list standard PERMIT_MANAGEMENT
 permit host 192.168.10.50
 permit 192.168.20.0 0.0.0.255
 exit

! Apply ACL to VTY lines
line vty 0 15
 access-class PERMIT_MANAGEMENT in
 exit

```

### Extended IPv4 ACL (Filter based on Source, Destination, Protocol, & Port - place near source)

```cisco
ip access-list extended BLOCK_WEB_TO_SERVER
 ! Block LAN subnet from accessing HTTP/HTTPS on Server 10.0.0.100
 deny tcp 192.168.10.0 0.0.0.255 host 10.0.0.100 eq 80
 deny tcp 192.168.10.0 0.0.0.255 host 10.0.0.100 eq 443
 permit ip any any
 exit

! Apply inbound on router interface facing source LAN
interface GigabitEthernet 0/0/0
 ip access-group BLOCK_WEB_TO_SERVER in
 exit

```

---

## 3. Network Address Translation (NAT)

NAT maps private IPv4 addresses to public IPv4 addresses for internet connectivity.

### Dynamic NAT with Port Address Translation (PAT / Overload)

```cisco
! Step 1: Define internal traffic allowed to be translated
ip access-list standard NAT_ACL
 permit 192.168.0.0 0.0.255.255
 exit

! Step 2: Configure PAT overload on public WAN interface
ip nat inside source list NAT_ACL interface GigabitEthernet 0/0/1 overload

! Step 3: Identify Inside and Outside interfaces
interface GigabitEthernet 0/0/0
 ip nat inside
 exit

interface GigabitEthernet 0/0/1
 ip nat outside
 exit

```

### Static NAT (1-to-1 Mapping for Internal Servers)

```cisco
! Static 1:1 mapping: Internal Server <-> Public IP
ip nat inside source static 192.168.10.100 203.0.113.10

```

---

## 4. WAN Concepts & Site-to-Site VPNs

Connecting remote branch offices securely across untrusted public networks.

### IPsec Site-to-Site VPN Configuration

```cisco
! Step 1: ISAKMP (Phase 1) Policy
crypto isakmp policy 10
 encr aes 256
 hash sha256
 authentication pre-share
 group 14
 exit

crypto isakmp key SecretKey123 address 203.0.113.2

! Step 2: IPsec Transform Set (Phase 2)
crypto ipsec transform-set ESP-AES-SHA esp-aes 256 esp-sha256-hmac

! Step 3: Crypto Map matching interest traffic
ip access-list extended VPN_TRAFFIC
 permit ip 192.168.10.0 0.0.0.255 192.168.20.0 0.0.0.255
 exit

crypto map MY_VPN_MAP 10 ipsec-isakmp
 set peer 203.0.113.2
 set transform-set ESP-AES-SHA
 match address VPN_TRAFFIC
 exit

! Step 4: Apply Crypto Map to WAN Interface
interface GigabitEthernet 0/0/1
 crypto map MY_VPN_MAP
 exit

```

---

## 5. Network Management (NTP, Syslog, SNMP)

Monitoring, logging, and time synchronization across infrastructure devices.

```cisco
! NTP Time Synchronization
ntp server 203.0.113.50

! Syslog Logging to Central Server
logging host 192.168.10.250
logging trap warnings

! SNMPv2c Community Read-Only Access
snmp-server community READONLY_COMM ro
snmp-server location Lab_Rack_1
snmp-server contact admin@lab.local

```

---

## 6. Network Automation, SDN & REST APIs

High-level concepts tested on CCNA 200-301 regarding software-defined networking, APIs, and data encoding formats.

| Topic | Key Concept |
| --- | --- |
| **Control Plane vs. Data Plane** | Control Plane (Routing decisions/OSPF/STP) vs. Data Plane (Packet forwarding via ASIC). |
| **SDN Architecture** | Overlay/Underlay networks, Cisco DNA Center, Centralized Controller managing Southbound (OpenFlow/NETCONF) and Northbound (REST APIs) interfaces. |
| **REST APIs** | Uses HTTP methods: `GET` (Read), `POST` (Create), `PUT` (Update), `DELETE` (Remove). |
| **Data Formats** | **JSON** (Key/Value pairs with `{}` and `[]`), **YAML** (Indentation-based), **XML** (Tag-based `<tag>`). |

---

## 7. Verification & Troubleshooting Commands

Essential diagnostic commands for OSPF, NAT, ACLs, and system health in Module 3.

```cisco
! OSPF Verification
show ip ospf neighbor
show ip ospf interface brief
show ip route ospf

! NAT Verification
show ip nat translations
show ip nat statistics

! Security & ACL Verification
show access-lists

! Network Management & Services Verification
show ntp status
show ntp associations

```

---

## 📂 Related Labs

Check out the Packet Tracer `.pkt` files inside the [`/labs`](https://www.google.com/search?q=./labs) directory to test these configurations interactively!

---