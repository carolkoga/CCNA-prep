# Module 1: VLSM Practice Exercises

---

## Questions

### Question 1: Sorting & Optimal Mask Selection

You are allocated the block **`192.168.10.0 /24`**. You need to design subnets for three departments:

* **Department A:** 28 hosts
* **Department B:** 60 hosts
* **Department C:** 12 hosts

1. In what order must these subnets be allocated?
2. What CIDR prefix (`/XX`) should be assigned to each department to minimize address waste?

**[Jump to Solution 1](#solution-for-question-1)**

---

### Question 2: Simple Sequential VLSM Allocation

Using the base network **`10.1.1.0 /24`**, allocate subnets sequentially for the following requirements (from largest to smallest):

1. **LAN A:** 100 hosts
2. **LAN B:** 50 hosts
3. **LAN C:** 25 hosts

Find the **Network ID**, **Usable Host Range**, and **Broadcast Address** for each LAN.

**[Jump to Solution 2](#solution-for-question-2)**

---

### Question 3: Incorporating Point-to-Point Links (`/30`)

A branch office receives the block **`172.16.5.0 /24`**. Design subnets for:

* **HR VLAN:** 55 hosts
* **Finance VLAN:** 25 hosts
* **WAN Link 1 (Router to Router):** 2 hosts
* **WAN Link 2 (Router to Router):** 2 hosts

Provide the **Network ID** and **Prefix Length** for all 4 allocations.

**[Jump to Solution 3](#solution-for-question-3)**

---

### Question 4: Identifying VLSM Overlap / Conflicts

An administrator configures three subnets from the `192.168.1.0/24` parent block:

* **Subnet 1:** `192.168.1.0 /25`
* **Subnet 2:** `192.168.1.96 /27`
* **Subnet 3:** `192.168.1.128 /26`

Is there an address overlap between any of these subnets? If yes, identify which subnets conflict and explain why.

**[Jump to Solution 4](#solution-for-question-4)**

---

### Question 5: Modern Point-to-Point Links (`/31` vs `/30`)

Per **RFC 3021**, modern routers can use `/31` masks on point-to-point links.

1. What is the Subnet Mask of a `/31` in dotted-decimal?
2. If two routers are connected via `10.0.0.0 /31`, what are the usable IP addresses for Router A and Router B?

**[Jump to Solution 5](#solution-for-question-5)**

---

### Question 6: Finding the Next Available VLSM Block

An enterprise network has allocated the following subnets from `10.50.0.0 /16`:

* **Subnet 1:** `10.50.0.0 /22`
* **Subnet 2:** `10.50.4.0 /23`

What is the **exact starting Network ID** for the next available `/24` subnet?

**[Jump to Solution 6](#solution-for-question-6)**

---

### Question 7: Subnetting Across Octet Boundaries (3rd Octet VLSM)

You are given **`172.20.0.0 /16`**. Allocate subnets for:

1. **Engineering:** 1,000 hosts
2. **Sales:** 450 hosts
3. **Management:** 200 hosts

Find the **Network ID** and **Subnet Mask** for each.

**[Jump to Solution 7](#solution-for-question-7)**

---

### Question 8: Calculating Unallocated Space

You are given a `/24` parent block (`192.168.5.0/24`). You allocate:

* One `/25` subnet
* One `/26` subnet
* Two `/28` subnets

How many **unused IP addresses** remain in the `192.168.5.0/24` parent block?

**[Jump to Solution 8](#solution-for-question-8)**

---

### Question 9: Validating Host Membership in VLSM

A host is configured with IP **`172.16.18.75`** and mask **`255.255.240.0`** (`/20`).
Does another host with IP **`172.16.31.250 /20`** reside on the exact same subnet? Explain using block boundaries.

**[Jump to Solution 9](#solution-for-question-9)**

---

### Question 10: Multi-Site Enterprise Scenario

Company X has the core network **`10.100.0.0 /16`**.

* **Site A** requires capacity for **2,000 hosts**.
* **Site B** requires capacity for **500 hosts**.
* **Site C** requires capacity for **250 hosts**.

Allocate the network blocks sequentially starting from `10.100.0.0` and list their **Broadcast Addresses**.

**[Jump to Solution 10](#solution-for-question-10)**

---

### Question 11: VLSM Route Summarization

A router learns four contiguous VLSM subnets via OSPF:

* `192.168.16.0 /24`
* `192.168.17.0 /24`
* `192.168.18.0 /24`
* `192.168.19.0 /24`

What is the single **summary route (supernet)** with CIDR prefix that represents all four subnets?

**[Jump to Solution 11](#solution-for-question-11)**

---

### Question 12: Reverse VLSM Design (Troubleshooting)

A junior engineer assigned the following IPs to interfaces on a single router:

* `Gig0/0`: `10.0.0.1 /27`
* `Gig0/1`: `10.0.0.33 /28`
* `Gig0/2`: `10.0.0.49 /29`

Is this interface addressing scheme valid, or is there an overlap?

**[Jump to Solution 12](#solution-for-question-12)**

---

## Solutions & Detailed Explanations

---

### Solution for Question 1

#### Answer:

1. **Allocation Order:** Department B (60) $\rightarrow$ Department A (28) $\rightarrow$ Department C (12)
2. **Prefixes:** Department B = **/26**, Department A = **/27**, Department C = **/28**

#### Step-by-Step Explanation:

* **Golden Rule of VLSM:** Always allocate from **largest to smallest** host requirement.
* **Department B (60 hosts):** $2^h - 2 \ge 60 \rightarrow 2^6 - 2 = 62 \text{ hosts}$. Needs 6 host bits $\rightarrow 32 - 6 = \mathbf{/26}$.
* **Department A (28 hosts):** $2^h - 2 \ge 28 \rightarrow 2^5 - 2 = 30 \text{ hosts}$. Needs 5 host bits $\rightarrow 32 - 5 = \mathbf{/27}$.
* **Department C (12 hosts):** $2^h - 2 \ge 12 \rightarrow 2^4 - 2 = 14 \text{ hosts}$. Needs 4 host bits $\rightarrow 32 - 4 = \mathbf{/28}$.

↩️ **[Back to Question 1](#question-1-sorting--optimal-mask-selection)** | ➡️ **[Go to Question 2](#question-2-simple-sequential-vlsm-allocation)**

---

### Solution for Question 2

#### Answer:

* **LAN A (`/25`):** Network `10.1.1.0/25` | Range `10.1.1.1 – 10.1.1.126` | Broadcast `10.1.1.127`
* **LAN B (`/26`):** Network `10.1.1.128/26` | Range `10.1.1.129 – 10.1.1.190` | Broadcast `10.1.1.191`
* **LAN C (`/27`):** Network `10.1.1.192/27` | Range `10.1.1.193 – 10.1.1.222` | Broadcast `10.1.1.223`

#### Step-by-Step Explanation:

1. **LAN A (100 hosts):** Requires `/25` (Block Size = 128).
* Spans `.0` to `.127`. Next free IP: `.128`.


2. **LAN B (50 hosts):** Requires `/26` (Block Size = 64).
* Starts at `.128`. Spans `.128` to `.191`. Next free IP: `.192`.


3. **LAN C (25 hosts):** Requires `/27` (Block Size = 32).
* Starts at `.192`. Spans `.192` to `.223`.



↩️ **[Back to Question 2](#question-2-simple-sequential-vlsm-allocation)** | ➡️ **[Go to Question 3](#question-3-incorporating-point-to-point-links-30)**

---

### Solution for Question 3

#### Answer:

* **HR VLAN:** `172.16.5.0 /26`
* **Finance VLAN:** `172.16.5.64 /27`
* **WAN Link 1:** `172.16.5.96 /30`
* **WAN Link 2:** `172.16.5.100 /30`

#### Step-by-Step Explanation:

1. **HR (55 hosts):** Needs `/26` (Block Size = 64). Network: `172.16.5.0 /26` (Broadcast: `.63`).
2. **Finance (25 hosts):** Needs `/27` (Block Size = 32). Starts at `.64`. Network: `172.16.5.64 /27` (Broadcast: `.95`).
3. **WAN Link 1 (2 hosts):** Needs `/30` (Block Size = 4). Starts at `.96`. Network: `172.16.5.96 /30` (Broadcast: `.99`).
4. **WAN Link 2 (2 hosts):** Needs `/30` (Block Size = 4). Starts at `.100`. Network: `172.16.5.100 /30` (Broadcast: `.103`).

↩️ **[Back to Question 3](#question-3-incorporating-point-to-point-links-30)** | ➡️ **[Go to Question 4](#question-4-identifying-vlsm-overlap--conflicts)**

---

### Solution for Question 4

#### Answer:

**Yes, Subnet 1 and Subnet 2 overlap.**

#### Step-by-Step Explanation:

* **Subnet 1 (`192.168.1.0 /25`):** Block size = 128. Range: `192.168.1.0` to `192.168.1.127`.
* **Subnet 2 (`192.168.1.96 /27`):** Range: `192.168.1.96` to `192.168.1.127`.
* **Conflict:** Subnet 2 falls completely inside the IP range already claimed by Subnet 1 (`.0` to `.127`). Subnet 2 should have been started at `.128` or higher.

↩️ **[Back to Question 4](#question-4-identifying-vlsm-overlap--conflicts)** | ➡️ **[Go to Question 5](#question-5-modern-point-to-point-links-31-vs-30)**

---

### Solution for Question 5

#### Answer:

1. **Subnet Mask:** `255.255.255.254`
2. **Usable IPs:** Router A = `10.0.0.0`, Router B = `10.0.0.1`

#### Step-by-Step Explanation:

1. A `/31` has 31 bits on and 1 host bit off ($2^1 = 2 \text{ IPs total}$).
* Mask: `11111111.11111111.11111111.11111110` = `255.255.255.254`.


2. RFC 3021 eliminates the standard rule subtracting Network ID and Broadcast for point-to-point links. Both addresses (`.0` and `.1`) become valid usable host IPs on the link!

↩️ **[Back to Question 5](#question-5-modern-point-to-point-links-31-vs-30)** | ➡️ **[Go to Question 6](#question-6-finding-the-next-available-vlsm-block)**

---

### Solution for Question 6

#### Answer:

**`10.50.6.0 /24`**

#### Step-by-Step Explanation:

1. **Subnet 1 (`10.50.0.0 /22`):** Block size in 3rd octet = $256 - 252 = 4$.
* Spans `10.50.0.0` to `10.50.3.255`. Next free IP: `10.50.4.0`.


2. **Subnet 2 (`10.50.4.0 /23`):** Block size in 3rd octet = $256 - 254 = 2$.
* Spans `10.50.4.0` to `10.50.5.255`. Next free IP: `10.50.6.0`.


3. The next available starting Network ID for any mask is **`10.50.6.0`**.

↩️ **[Back to Question 6](#question-6-finding-the-next-available-vlsm-block)** | ➡️ **[Go to Question 7](#question-7-subnetting-across-octet-boundaries-3rd-octet-vlsm)**

---

### Solution for Question 7

#### Answer:

* **Engineering (1000 hosts):** Network `172.20.0.0 /22` | Mask `255.255.252.0`
* **Sales (450 hosts):** Network `172.20.4.0 /23` | Mask `255.255.254.0`
* **Management (200 hosts):** Network `172.20.6.0 /24` | Mask `255.255.255.0`

#### Step-by-Step Explanation:

1. **Engineering (1000 hosts):** $2^{10} - 2 = 1022$ hosts $\rightarrow 10$ host bits $\rightarrow$ Prefix `/22` ($32 - 10$). 3rd Octet Block Size = 4. Range: `172.20.0.0` to `172.20.3.255`.
2. **Sales (450 hosts):** $2^9 - 2 = 510$ hosts $\rightarrow 9$ host bits $\rightarrow$ Prefix `/23`. Starts at `172.20.4.0`. 3rd Octet Block Size = 2. Range: `172.20.4.0` to `172.20.5.255`.
3. **Management (200 hosts):** $2^8 - 2 = 254$ hosts $\rightarrow 8$ host bits $\rightarrow$ Prefix `/24`. Starts at `172.20.6.0`.

↩️ **[Back to Question 7](#question-7-subnetting-across-octet-boundaries-3rd-octet-vlsm)** | ➡️ **[Go to Question 8](#question-8-calculating-unallocated-space)**

---

### Solution for Question 8

#### Answer:

**32 unused IP addresses**

#### Step-by-Step Explanation:

* A `/24` parent block contains **256 total IPs**.
* **One `/25`:** Uses 128 IPs.
* **One `/26`:** Uses 64 IPs.
* **Two `/28`s:** $16 + 16 = 32$ IPs.
* **Total Used IPs:** $128 + 64 + 32 = 224 \text{ IPs}$.
* **Unallocated IPs:** $256 - 224 = \mathbf{32 \text{ IPs}}$ (which form one free `/27` block!).

↩️ **[Back to Question 8](#question-8-calculating-unallocated-space)** | ➡️ **[Go to Question 9](#question-9-validating-host-membership-in-vlsm)**

---

### Solution for Question 9

#### Answer:

**Yes, both hosts belong to the same subnet (`172.16.16.0 /20`).**

#### Step-by-Step Explanation:

1. **Mask `/20` (`255.255.240.0`):** 3rd Octet Block Size = $256 - 240 = \mathbf{16}$.
2. Subnets increment by 16 in the 3rd octet:
* Subnet 1: `172.16.0.0 /20` (`172.16.0.0` to `172.16.15.255`)
* Subnet 2: **`172.16.16.0 /20`** (`172.16.16.0` to `172.16.31.255`)


3. Both `172.16.18.75` and `172.16.31.250` fall between `172.16.16.0` and `172.16.31.255`.

↩️ **[Back to Question 9](#question-9-validating-host-membership-in-vlsm)** | ➡️ **[Go to Question 10](#question-10-multi-site-enterprise-scenario)**

---

### Solution for Question 10

#### Answer:

* **Site A (`/21`):** Network `10.100.0.0 /21` | Broadcast: `10.100.7.255`
* **Site B (`/23`):** Network `10.100.8.0 /23` | Broadcast: `10.100.9.255`
* **Site C (`/24`):** Network `10.100.10.0 /24` | Broadcast: `10.100.10.255`

#### Step-by-Step Explanation:

1. **Site A (2,000 hosts):** Requires $2^{11} - 2 = 2046$ hosts $\rightarrow$ Prefix **/21** (3rd Octet Block Size = 8). Range: `10.100.0.0` to `10.100.7.255`.
2. **Site B (500 hosts):** Requires $2^9 - 2 = 510$ hosts $\rightarrow$ Prefix **/23** (3rd Octet Block Size = 2). Starts at `10.100.8.0`. Range: `10.100.8.0` to `10.100.9.255`.
3. **Site C (250 hosts):** Requires $2^8 - 2 = 254$ hosts $\rightarrow$ Prefix **/24** (3rd Octet Block Size = 1). Starts at `10.100.10.0`. Range: `10.100.10.0` to `10.100.10.255`.

↩️ **[Back to Question 10](#question-10-multi-site-enterprise-scenario)** | ➡️ **[Go to Question 11](#question-11-vlsm-route-summarization)**

---

### Solution for Question 11

#### Answer:

**`192.168.16.0 /22`**

#### Step-by-Step Explanation:

Look at the 3rd octets in binary:

* `16` = `000100` `00`
* `17` = `000100` `01`
* `18` = `000100` `10`
* `19` = `000100` `11`

The first 6 bits of the 3rd octet (`000100`) are identical across all four routes.

* Matching bits: $8 \text{ (1st octet)} + 8 \text{ (2nd octet)} + 6 \text{ (3rd octet)} = \mathbf{22 \text{ bits}}$.
* **Summary Route:** `192.168.16.0 /22`.

↩️ **[Back to Question 11](#question-11-vlsm-route-summarization)** | ➡️ **[Go to Question 12](#question-12-reverse-vlsm-design-troubleshooting)**

---

### Solution for Question 12

#### Answer:

**The configuration is valid! There are NO overlapping addresses.**

#### Step-by-Step Explanation:

* **`Gig0/0` (`10.0.0.1 /27`):** Subnet range is `10.0.0.0` to `10.0.0.31` (Block size 32). Next free IP: `.32`.
* **`Gig0/1` (`10.0.0.33 /28`):** Subnet range is `10.0.0.32` to `10.0.0.47` (Block size 16). Next free IP: `.48`.
* **`Gig0/2` (`10.0.0.49 /29`):** Subnet range is `10.0.0.48` to `10.0.0.55` (Block size 8).

All three subnets sit neatly side-by-side without a single overlapping bit!

↩️ **[Back to Question 12](#question-12-reverse-vlsm-design-troubleshooting)**

---