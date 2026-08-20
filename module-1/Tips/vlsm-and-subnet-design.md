# 🍰 VLSM (Variable Length Subnet Masking) Explained

In traditional classful or fixed-length subnetting (FLSM), every subnet uses the exact same mask size. While simple, FLSM wastes millions of IP addresses.

**Variable Length Subnet Masking (VLSM)** solves this problem by allowing network engineers to use different subnet masks across the same network block, customizing subnet sizes according to specific host requirements.

---

## The Golden Rule of VLSM

> **Always allocate subnets from LARGEST requirement to SMALLEST requirement.**

If you attempt to assign smaller subnets before larger ones, subnet boundaries will overlap, leading to IP address conflicts and broken routing tables.

---

## Step-by-Step VLSM Process

To design a VLSM network:

1. **List all host requirements** for each department/vlan.
2. **Sort requirements in descending order** (highest number of hosts to lowest).
3. **Determine the appropriate CIDR prefix (`/XX`)** and **Block Size** for each requirement using $2^h - 2 \ge \text{Hosts Required}$.
4. **Assign Network IDs sequentially**, starting from the base address and incrementing by the current subnet's **Block Size**.

---

## Practical Example

### Scenario Requirements

You are allocated the Class C network block **`192.168.1.0 /24`** (256 total IP addresses). You need to design subnets for four distinct network segments:

* **Sales VLAN:** 100 hosts
* **IT VLAN:** 50 hosts
* **Executive VLAN:** 20 hosts
* **Router Point-to-Point Link:** 2 hosts

---

### Step 1: Sort Requirements & Determine Mask Sizes

| Segment | Hosts Needed | Formula ($2^h - 2 \ge \text{Hosts}$) | Host Bits ($h$) | Prefix / Mask | Block Size ($2^h$) | Usable Hosts ($2^h - 2$) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **1. Sales** | 100 | $2^7 - 2 = 126$ | 7 | **/25** (`255.255.255.128`) | **128** | 126 |
| **2. IT** | 50 | $2^6 - 2 = 62$ | 6 | **/26** (`255.255.255.192`) | **64** | 62 |
| **3. Executive** | 20 | $2^5 - 2 = 30$ | 5 | **/27** (`255.255.255.224`) | **32** | 30 |
| **4. P2P Link** | 2 | $2^2 - 2 = 2$ | 2 | **/30** (`255.255.255.252`) | **4** | 2 |

---

### Step 2: Sequential Subnet Allocation

Start at **`192.168.1.0`** and allocate blocks sequentially using each segment's respective block size:

#### 1. Sales VLAN (`/25` — Block Size = 128)
* **Network ID:** `192.168.1.0 /25`
* **Usable Host Range:** `192.168.1.1` to `192.168.1.126`
* **Broadcast Address:** `192.168.1.127`
* *Next available IP:* `192.168.1.128`

#### 2. IT VLAN (`/26` — Block Size = 64)
* **Network ID:** `192.168.1.128 /26`
* **Usable Host Range:** `192.168.1.129` to `192.168.1.190`
* **Broadcast Address:** `192.168.1.191`
* *Next available IP:* `192.168.1.192`

#### 3. Executive VLAN (`/27` — Block Size = 32)
* **Network ID:** `192.168.1.192 /27`
* **Usable Host Range:** `192.168.1.193` to `192.168.1.222`
* **Broadcast Address:** `192.168.1.223`
* *Next available IP:* `192.168.1.224`

#### 4. Point-to-Point Router Link (`/30` — Block Size = 4)
* **Network ID:** `192.168.1.224 /30`
* **Usable Host Range:** `192.168.1.225` and `192.168.1.226`
* **Broadcast Address:** `192.168.1.227`
* *Remaining Unallocated Space:* `192.168.1.228` to `192.168.1.255` (28 unused IPs saved for future growth!)

---

## 🗺️ Visual Address Space Map (`192.168.1.0/24`)

```text
0                                                                  127 128                                191 192                     223 224              227 228                 255
[======================= Sales /25 (128 IPs) =======================][========== IT /26 (64 IPs) ==========][== Exec /27 (32 IPs) ==][ Link /30 (4 IPs) ][ Free Space (28 IPs) ]