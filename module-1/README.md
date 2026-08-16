```markdown
## 🌐 CCNA Module 1: Introduction to Networks (ITN)

Welcome to the **CCNA Module 1 (ITN)** study guide and lab reference! This repository contains a curated collection of foundational Cisco IOS commands, syntax examples, and lab verification procedures essential for passing the Cisco CCNA (200-301) exam.

---

## 📌 Table of Contents
- [1. Initial Access & Basic Device Configuration](#1-initial-access--basic-device-configuration)
- [2. Remote Access Configuration (SSH)](#2-remote-access-configuration-ssh)
- [3. IP Addressing & SVI Configuration](#3-ip-addressing--svi-configuration)
- [4. Verification, Diagnostics & Memory Management](#4-verification-diagnostics--memory-management)

---

## 1. Initial Access & Basic Device Configuration

These commands establish the baseline security posture, device identity, and access controls for switches and routers.

```cisco
! Enter Privileged EXEC and Global Configuration modes
enable
configure terminal

! Set device hostname
hostname SW-A1

! Set encrypted Privileged EXEC password
enable secret cisco123

! Secure the Console line access
line console 0
 password ciscoconsole
 login
 exit

! Encrypt all plaintext passwords stored in running-config
service password-encryption

! Configure a Message of the Day (MOTD) banner
banner motd # Unauthorized Access is Strictly Prohibited! #

```

---

## 2. Remote Access Configuration (SSH)

Securing management traffic over the network requires replacing Telnet with SSH version 2.

```cisco
! Step 1: Configure domain name and generate RSA keys
ip domain-name lab.local
crypto key generate rsa general-keys modulus 1024

! Step 2: Enforce SSH version 2
ip ssh version 2

! Step 3: Create a local administrative user
username admin secret admin123

! Step 4: Restrict VTY lines to SSH and local authentication
line vty 0 15
 transport input ssh
 login local
 exit

```

> **Note:** Always ensure a hostname and domain name are set before generating RSA keys.

---

## 3. IP Addressing & SVI Configuration

Assigning IPv4 and IPv6 addresses to router physical interfaces and switch Virtual Interfaces (SVI) enables network layer communication and remote management.

### Router Interface Configuration (IPv4 & IPv6)

```cisco
interface gigabitethernet 0/0/0
 description Connection to Local Area Network
 ip address 192.168.1.1 255.255.255.0
 ipv6 address 2001:db8:acad:1::1/64
 ipv6 address fe80::1 link-local
 no shutdown
 exit

```

### Switch Virtual Interface (SVI) Configuration (IPv4 Management)

```cisco
interface vlan 1
 description Management SVI for Switch
 ip address 192.168.1.2 255.255.255.0
 no shutdown
 exit

! Set the default gateway for out-of-subnet management
ip default-gateway 192.168.1.1

```

---

## 4. Verification, Diagnostics & Memory Management

Essential operational commands used to inspect interface states, review running configurations, and persist changes across device reboots.

### Interface & Configuration Auditing

```cisco
! Quick interface status summary
show ip interface brief
show ipv6 interface brief

! View active (RAM) vs. startup (NVRAM) configurations
show running-config
show startup-config

```

### Saving Configuration to NVRAM

```cisco
! Primary command
copy running-config startup-config

! Shorthand alias
write memory

```

### Network Connectivity Testing

```cisco
! Test L3 reachability
ping 192.168.1.1

! Trace route path across hops
traceroute 192.168.1.1

```

---

## 📂 Related Labs

Check out the Packet Tracer `.pkt` files inside the [`/labs`](https://www.google.com/search?q=./labs) directory to test these configurations interactively!

```

<ElicitationsGroup message="What would you like to set up next for your repo?">
  <Elicitation label="Create a main root README.md with course progress trackers" query="Generate a main README.md for the root directory of the repository with progress checkboxes, module index, and badges."/>
  <Elicitation label="Generate a .gitignore file for Packet Tracer and Cisco files" query="Give me a standard .gitignore file template customized for Cisco Packet Tracer and Cisco lab files."/>
</ElicitationsGroup>

```