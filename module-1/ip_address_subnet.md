# 🧮 CCNA IP Addressing & Subnetting Cheatsheet

A quick-reference guide for IPv4 subnetting, CIDR notation, IPv6 fundamentals, and essential IP concepts required for the Cisco CCNA (200-301) exam.

---

## 📌 Table of Contents
- [1. Subnet Mask & CIDR Conversion Table](#1-subnet-mask--cidr-conversion-table)
- [2. Powers of 2 & Subnetting Block Sizes](#2-powers-of-2--subnetting-block-sizes)
- [3. IPv4 Address Classes & Special Ranges](#3-ipv4-address-classes--special-ranges)
- [4. Essential Formulas for Subnetting](#4-essential-formulas-for-subnetting)
- [5. IPv6 Fundamentals & Essential Prefixes](#5-ipv6-fundamentals--essential-prefixes)

---

## 1. Subnet Mask & CIDR Conversion Table

| CIDR Prefix | Subnet Mask | Wildcard Mask | Total IPs | Usable Hosts |
| :--- | :--- | :--- | :--- | :--- |
| **/32** | `255.255.255.255` | `0.0.0.0` | 1 | 1 (Host Route) |
| **/31** | `255.255.255.254` | `0.0.0.1` | 2 | 2 (Point-to-Point RFC 3021) |
| **/30** | `255.255.255.252` | `0.0.0.3` | 4 | 2 (Point-to-Point WAN) |
| **/29** | `255.255.255.248` | `0.0.0.7` | 8 | 6 |
| **/28** | `255.255.255.240` | `0.0.0.15` | 16 | 14 |
| **/27** | `255.255.255.224` | `0.0.0.31` | 32 | 30 |
| **/26** | `255.255.255.192` | `0.0.0.63` | 64 | 62 |
| **/25** | `255.255.255.128` | `0.0.0.127` | 128 | 126 |
| **/24** | `255.255.255.0` | `0.0.0.255` | 256 | 254 |
| **/23** | `255.255.254.0` | `0.0.1.255` | 512 | 510 |
| **/22** | `255.255.252.0` | `0.0.3.255` | 1,024 | 1,022 |
| **/21** | `255.255.248.0` | `0.0.7.255` | 2,048 | 2,046 |
| **/20** | `255.255.240.0` | `0.0.15.255` | 4,096 | 4,094 |
| **/19** | `255.255.224.0` | `0.0.31.255` | 8,192 | 8,190 |
| **/18** | `255.255.192.0` | `0.0.63.255` | 16,384 | 16,382 |
| **/17** | `255.255.128.0` | `0.0.127.255` | 32,768 | 32,766 |
| **/16** | `255.255.0.0` | `0.0.255.255` | 65,536 | 65,534 |
| **/8** | `255.0.0.0` | `0.255.255.255` | 16,777,216 | 16,777,214 |

---

## 2. Powers of 2 & Subnetting Block Sizes

Mastering these binary magic numbers allows you to solve subnetting questions quickly during the exam.

| Bit Position | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Octet Value** | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |
| **Block Size** | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

* **Magic Number Rule:** $\text{Block Size} = 256 - \text{Interesting Octet Subnet Mask Value}$  
  *(Example: For `255.255.255.224`, Block Size $= 256 - 224 = 32$. Subnets increase in increments of 32).*

---

## 3. IPv4 Address Classes & Special Ranges

### Classful Ranges
* **Class A:** `1.0.0.0` – `127.255.255.255` (Default `/8`)
* **Class B:** `128.0.0.0` – `191.255.255.255` (Default `/16`)
* **Class C:** `192.0.0.0` – `223.255.255.255` (Default `/24`)
* **Class D (Multicast):** `224.0.0.0` – `239.255.255.255`
* **Class E (Experimental):** `240.0.0.0` – `255.255.255.255`

### Private IPv4 Ranges (RFC 1918)
Non-routable on the public internet; used inside private local networks:
* **Class A Private:** `10.0.0.0` – `10.255.255.255` (`10.0.0.0/8`)
* **Class B Private:** `172.16.0.0` – `172.31.255.255` (`172.16.0.0/12`)
* **Class C Private:** `192.168.0.0` – `192.168.255.255` (`192.168.0.0/16`)

### Special IPv4 Addresses
* **Loopback:** `127.0.0.0/8` (Used for local interface self-testing, e.g., `127.0.0.1`).
* **APIPA (Automatic Private IP):** `169.254.0.0/16` (Assigned automatically by Windows/OS when DHCP fails).
* **Default Route / Any:** `0.0.0.0/0`
* **Local Broadcast:** `255.255.255.255`

---

## 4. Essential Formulas for Subnetting

1. **Calculate Usable Hosts per Subnet:**
   $$\text{Usable Hosts} = 2^h - 2$$
   *(Where $h$ is the number of host bits remaining).*

2. **Calculate Number of Created Subnets:**
   $$\text{Number of Subnets} = 2^s$$
   *(Where $s$ is the number of borrowed subnet bits).*

3. **Wildcard Mask Calculation:**
   $$\text{Wildcard Mask} = 255.255.255.255 - \text{Subnet Mask}$$
   *(Example: $255.255.255.255 - 255.255.255.240 = 0.0.0.15$).*

---

## 5. IPv6 Fundamentals & Essential Prefixes

IPv6 addresses are **128 bits** long, written in hexadecimal, separated by colons into 8 hextets of 16 bits each.

### IPv6 Address Types & Prefixes
* **Global Unicast Address (GUA):** `2000::/3` (Routable on the public internet; equivalent to public IPv4).
* **Link-Local Address:** `fe80::/10` (Mandatory on every active interface; auto-configured or static, non-routable beyond local link).
* **Unique Local Address (ULA):** `fc00::/7` / `fd00::/8` (Equivalent to RFC 1918 private IPv4 addresses).
* **Loopback Address:** `::1/128` (Equivalent to `127.0.0.1`).
* **Unspecified Address:** `::/128` (Equivalent to `0.0.0.0`).
* **Multicast Address:** `ff00::/8`
  * `ff02::1` = All-nodes multicast group (all IPv6 devices on link).
  * `ff02::2` = All-routers multicast group.
  * `ff02::5` / `ff02::6` = OSPFv3 routers.

### IPv6 Compression Rules
1. **Omit Leading Zeros:** `0db8` $\rightarrow$ `db8`, `0001` $\rightarrow$ `1`.
2. **Double Colon (`::`):** Replace consecutive blocks of all-zero hextets with `::` **once per address**.
   * *Example:* `2001:0db8:0000:0000:0000:0000:0000:0001` $\rightarrow$ `2001:db8::1`.