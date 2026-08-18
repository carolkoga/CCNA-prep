# Binary, Subnetting, and Subnet Masks Fundamentals

Understanding how IP addressing works at the **binary level** is the single most important skill for passing the Cisco CCNA (200-301) exam and working in real-world network engineering.

Instead of memorizing random decimal numbers, this guide breaks down the core concepts of **bits, bytes, network portions, host portions, and subnet masks**.

---

## 1. Bits, Bytes, and Octets

Computers and networking devices process all data in binary (**0s and 1s**).

* **Bit (Binary Digit):** The smallest unit of data ($0$ or $1$).
* **Byte:** A group of **8 bits**.
* **Octet:** In networking, an IPv4 address consists of **32 total bits**, divided into **4 octets** (8 bits each) separated by dots.

$$\text{IPv4 Address} = \text{32 bits total} = \text{4 Octets} \times \text{8 bits}$$

### Binary to Decimal Example

```text
IPv4 in Binary:  11000000 . 10101000 . 00001010 . 00000001
IPv4 in Decimal:    192   .    168   .     10    .     1

```

---

## 2. The "Magic Table" of 8 Bits (Positional Values)

Because binary is a base-2 system, each of the 8 position slots in an octet carries a specific positional weight (powers of 2), read from **right to left**:

| Bit Position | Bit 7 | Bit 6 | Bit 5 | Bit 4 | Bit 3 | Bit 2 | Bit 1 | Bit 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Power of 2** | $2^7$ | $2^6$ | $2^5$ | $2^4$ | $2^3$ | $2^2$ | $2^1$ | $2^0$ |
| **Decimal Weight** | **128** | **64** | **32** | **16** | **8** | **4** | **2** | **1** |

> 💡 **Pro-Tip:** Memorize this 8-bit sequence: `128 - 64 - 32 - 16 - 8 - 4 - 2 - 1`. You will use it for every conversion on the exam!

### Conversions at a Glance:

* **All 0s (`00000000`):** Decimal `0` (Minimum octet value)
* **All 1s (`11111111`):** $128 + 64 + 32 + 16 + 8 + 4 + 2 + 1 =$ Decimal `255` (Maximum octet value)

---

## 3. How Subnet Masks Split Network and Host Portions

An IPv4 address alone is incomplete. It requires a **Subnet Mask** to tell the router where the **Network Portion** ends and the **Host Portion** begins.

### The Immutable Subnet Mask Rule:

* **Binary `1`s = Network Portion** (Defines the street/neighborhood)
* **Binary `0`s = Host Portion** (Defines the specific house number)

---

## 4. How Routers Find the Network ID: Logical AND Operation

When a router receives a packet, it performs a bitwise **`AND`** operation between the **Destination IP Address** and the **Subnet Mask** to extract the **Network ID**.

### Truth Table for Logical AND:

* $1 \text{ AND } 1 = \mathbf{1}$
* $1 \text{ AND } 0 = \mathbf{0}$
* $0 \text{ AND } 0 = \mathbf{0}$

### Practical Example: `192.168.10.50 /24`

In **CIDR notation**, `/24` means the first 24 bits are contiguous `1`s (`255.255.255.0`).

```text
IP Address:     11000000 . 10101000 . 00001010 . 00110010  (192.168.10.50)
Subnet Mask:    11111111 . 11111111 . 11111111 . 00000000  (255.255.255.0 /24)
                |-----------------------------| |-------|
                     24 NETWORK BITS             8 HOST BITS

Bitwise AND:    11000000 . 10101000 . 00001010 . 00000000
Network ID:        192   .    168   .     10    .     0    => 192.168.10.0

```

---

## 5. Subnet Mask Progression Cheat Sheet

Subnet masks always consist of contiguous `1`s starting from the left. Here is how mask octets are formed as bits are turned on:

| CIDR Prefix (per octet) | Binary Pattern | Decimal Weight Addition | Subnet Mask Value |
| --- | --- | --- | --- |
| **/1** | `10000000` | $128$ | **128** |
| **/2** | `11000000` | $128 + 64$ | **192** |
| **/3** | `11100000` | $128 + 64 + 32$ | **224** |
| **/4** | `11110000` | $128 + 64 + 32 + 16$ | **240** |
| **/5** | `11111000` | $128 + 64 + 32 + 16 + 8$ | **248** |
| **/6** | `11111100` | $128 + 64 + 32 + 16 + 8 + 4$ | **252** |
| **/7** | `11111110` | $128 + 64 + 32 + 16 + 8 + 4 + 2$ | **254** |
| **/8** | `11111111` | $128 + 64 + 32 + 16 + 8 + 4 + 2 + 1$ | **255** |

---

## 6. Key Formulas for CCNA Subnetting

When calculating subnets, remember these two essential formulas where $h$ is the number of **host bits (binary `0`s)** remaining in the mask:

1. **Total IP Addresses in Subnet:**

$$\text{Total IPs} = 2^h$$


2. **Usable Host Addresses:**

$$\text{Usable Hosts} = 2^h - 2$$


*(We subtract 2 because the **Network ID** [all 0s in host bits] and the **Broadcast Address** [all 1s in host bits] cannot be assigned to end devices).*

3. **Block Size (The "Magic Number" Method)**

The **Block Size** represents the total number of IP addresses contained in a subnet. It determines the "increment step" between consecutive subnets without requiring full binary conversion.

$$\text{Block Size} = 256 - \text{Interesting Octet Subnet Mask}$$

#### Why do we use 256 in the formula?
An 8-bit octet has **256 total possible value combinations** ($2^8 = 256$), ranging from `0` to `255`. Since the subnet mask consumes a portion of those bits starting from the left, subtracting the mask value from `256` reveals the exact number of remaining host address combinations in that octet block.

---

#### Examples

**Example 1: `/26` Subnet Mask (`255.255.255.192`)**
1. **Find the Interesting Octet:** The 4th octet (`192`).
2. **Calculate Block Size:** $256 - 192 = \mathbf{64}$.
3. **Determine Subnet Boundaries (Counting by 64 in the 4th octet):**
   * Subnet 1: `192.168.1.0` to `192.168.1.63`
   * Subnet 2: `192.168.1.64` to `192.168.1.127`
   * Subnet 3: `192.168.1.128` to `192.168.1.191`
   * Subnet 4: `192.168.1.192` to `192.168.1.255`

> **Host Lookup Example:** For IP `192.168.1.50 /26`, since `.50` falls between `.0` and `.63`, it belongs to **Subnet 1**:
> * **Network ID:** `192.168.1.0`
> * **Usable Range:** `192.168.1.1` – `192.168.1.62`
> * **Broadcast:** `192.168.1.63`

---

**Example 2: `/20` Subnet Mask (`255.255.240.0`)**
1. **Find the Interesting Octet:** The 3rd octet (`240`).
2. **Calculate Block Size:** $256 - 240 = \mathbf{16}$.
3. **Determine Subnet Boundaries (Counting by 16 in the 3rd octet):**
   * Subnet 1: `10.5.0.0` to `10.5.15.255`
   * Subnet 2: `10.5.16.0` to `10.5.31.255`
   * Subnet 3: `10.5.32.0` to `10.5.47.255`

> **Host Lookup Example:** For IP `10.5.20.100 /20`, since the 3rd octet value `20` falls between `16` and `31`, it belongs to **Subnet 2**:
> * **Network ID:** `10.5.16.0`
> * **Usable Range:** `10.5.16.1` – `10.5.31.254`
> * **Broadcast:** `10.5.31.255`

---

## IPv4 Fast Facts & Exam Trivia

* **The Max Value of 255:** The sum of all 8 bits in an octet ($128 + 64 + 32 + 16 + 8 + 4 + 2 + 1$) equals **255**. This is why no IPv4 octet can exceed 255.
* **The Sacrificed `127.0.0.0/8` Class:** The entire `127.0.0.0/8` block (16.7 million addresses) is reserved exclusively for internal loopback testing (e.g., `127.0.0.1`).
* **APIPA Addresses (`169.254.x.x`):** If a host gets a `169.254.x.x` address, it indicates that it failed to reach a DHCP server and self-assigned an **Automatic Private IP Address**.
* **Point-to-Point Links (`/30` vs `/31`):** Traditionally, point-to-point router links use `/30` (4 total IPs, 2 usable). However, **RFC 3021** permits `/31` masks on point-to-point links to eliminate address waste by treating Network ID and Broadcast as valid end IPs.
* **Total Global IPv4 Pool:** $2^{32} = \mathbf{4,294,967,296}$ total IPv4 addresses. Exhaustion of this pool led to widespread deployment of NAT and the transition to IPv6 ($2^{128}$).

---

## ⚡ Practice Exercises & Solutions

To test your understanding of binary conversions, subnet masks, and block size calculations, check out the step-by-step exercise guide:

🔗 [**Module 1: Bits, Bytes & Subnetting Practice Exercises**](https://github.com/carolkoga/CCNA-prep/tree/main/module-1/exercises/bits-bytes)