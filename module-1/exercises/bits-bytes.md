# Practice Exercises - Block 1 (Questions 1 to 5)

---

## Questions

### Question 1: Binary to Decimal Conversion

Convert the following 8-bit binary octet into its decimal equivalent: **`10110010`**.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-1)**

---

### Question 2: Decimal to Binary Conversion

Convert the decimal number **`205`** into an 8-bit binary octet.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-2)**

---

### Question 3: Network ID Extraction (Logical AND)

An administrator assigns an end device the IP address **`172.16.45.100`** with a subnet mask of **`255.255.240.0`** (`/20`). What is the **Network ID** of this subnet?

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-3)**

---

### Question 4: Usable Host Count Calculation

A network engineer needs to subnet a Class C network using the prefix length **`/28`**.

1. How many total host bits remain?
2. How many **usable host IP addresses** are available per subnet?

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-4)**

---

### Question 5: Finding Broadcast Address & Usable Range

Given the host IP address **`192.168.1.138 /27`**, determine:

1. The **Subnet Mask** in dotted-decimal format.
2. The **Network ID**.
3. The **Broadcast Address**.
4. The **Usable Host Range**.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-5)**

---

### Question 6: CIDR Prefix to Subnet Mask Conversion

Convert the CIDR prefix **`/22`** into its dotted-decimal subnet mask representation.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-6)**

---

### Question 7: Subnet Range in the 3rd Octet

Given the IP address **`10.20.130.45 /19`**, determine:

1. The **Subnet Mask** in dotted-decimal format.
2. The **Network ID**.
3. The **Broadcast Address**.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-7)**

---

### Question 8: Wildcard Mask Calculation

Calculate the **Wildcard Mask** for the subnet **`172.16.64.0 /18`**.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-8)**

---

### Question 9: Same Subnet Verification

An engineer configures **Host A (`192.168.1.67 /26`)** and **Host B (`192.168.1.130 /26`)**. Can Host A communicate directly with Host B without going through a router (Layer 3 device)? Explain why or why not based on their Network IDs.

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-9)**

---

### Question 10: Designing a Subnet for a Specific Host Requirement

You are assigned the network **`192.168.50.0 /24`** and need to create subnets that can support **at least 28 usable hosts** per department.

1. What is the smallest prefix length (`/CIDR`) that meets this requirement?
2. What is the **Block Size**?
3. What is the **Network ID** of the second subnet created?

**[Jump to Answer & Explanation](https://www.google.com/search?q=%23solution-10)**


---

## 🔍 Solutions & Detailed Explanations

---

### 🔍 Solution for Question 1

#### Answer: `178`

#### Step-by-Step Explanation:

To convert binary to decimal, align the 8 bits with their corresponding positional weight values ($128, 64, 32, 16, 8, 4, 2, 1$) and sum the weights where the bit is **`1`**:

| Bit Weight | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Binary Bit** | **1** | **0** | **1** | **1** | **0** | **0** | **1** | **0** |

$$\text{Calculation: } 128 + 32 + 16 + 2 = \mathbf{178}$$

↩️ **[Back to Question 1](https://www.google.com/search?q=%23question-1-binary-to-decimal-conversion)** | ➡️ **[Go to Question 2](https://www.google.com/search?q=%23question-2-decimal-to-binary-conversion)**

---

### 🔍 Solution for Question 2

#### Answer: `11001101`

#### Step-by-Step Explanation:

Compare the decimal value `205` against the positional weights from left to right:

1. `205 >= 128`? **Yes** $\rightarrow$ Bit = **1**. Remainder: $205 - 128 = 77$
2. `77 >= 64`? **Yes** $\rightarrow$ Bit = **1**. Remainder: $77 - 64 = 13$
3. `13 >= 32`? **No** $\rightarrow$ Bit = **0**. Remainder: $13$
4. `13 >= 16`? **No** $\rightarrow$ Bit = **0**. Remainder: $13$
5. `13 >= 8`? **Yes** $\rightarrow$ Bit = **1**. Remainder: $13 - 8 = 5$
6. `5 >= 4`? **Yes** $\rightarrow$ Bit = **1**. Remainder: $5 - 4 = 1$
7. `1 >= 2`? **No** $\rightarrow$ Bit = **0**. Remainder: $1$
8. `1 >= 1`? **Yes** $\rightarrow$ Bit = **1**. Remainder: $1 - 1 = 0$

$$\text{Binary Result: } \mathbf{11001101}$$

↩️ **[Back to Question 2](https://www.google.com/search?q=%23question-2-decimal-to-binary-conversion)** | ➡️ **[Go to Question 3](https://www.google.com/search?q=%23question-3-network-id-extraction-logical-and)**

---

### 🔍 Solution for Question 3

#### Answer: `172.16.32.0`

#### Step-by-Step Explanation:

**Method 1: Block Size (Magic Number)**

1. Identify the **Interesting Octet** in the subnet mask `255.255.240.0`: The 3rd octet (`240`).
2. Calculate the **Block Size**: $256 - 240 = \mathbf{16}$.
3. Count by 16s in the 3rd octet to find the subnet boundaries:
* Subnet 1: `172.16.0.0`
* Subnet 2: `172.16.16.0`
* Subnet 3: **`172.16.32.0`** (spans `172.16.32.0` to `172.16.47.255`)
* Subnet 4: `172.16.48.0`


4. Since the 3rd octet value of the IP is `45`, it falls directly into the **`172.16.32.0`** block.

**Method 2: Binary Bitwise AND**

* 3rd octet IP (`45`): `00101101`
* 3rd octet Mask (`240`): `11110000`
* Bitwise `AND` result: `00100000` = **`32`**

$$\text{Network ID: } \mathbf{172.16.32.0}$$

↩️ **[Back to Question 3](https://www.google.com/search?q=%23question-3-network-id-extraction-logical-and)** | ➡️ **[Go to Question 4](https://www.google.com/search?q=%23question-4-usable-host-count-calculation)**

---

### 🔍 Solution for Question 4

#### Answer:

1. **Host bits remaining:** `4` bits
2. **Usable host IPs:** `14` addresses

#### Step-by-Step Explanation:

1. An IPv4 address has **32 total bits**.
2. **Calculate Host Bits ($h$):**

$$h = 32 - 28 = \mathbf{4 \text{ host bits}}$$


3. **Calculate Total IP Addresses:**

$$\text{Total IPs} = 2^h = 2^4 = \mathbf{16 \text{ total addresses}}$$


4. **Calculate Usable Host IPs:**

$$\text{Usable Hosts} = 2^h - 2 = 16 - 2 = \mathbf{14 \text{ usable host IPs}}$$



*(Note: We subtract 2 to exclude the **Network ID** [all host bits set to `0`] and the **Broadcast Address** [all host bits set to `1`]).*

↩️ **[Back to Question 4](https://www.google.com/search?q=%23question-4-usable-host-count-calculation)** | ➡️ **[Go to Question 5](https://www.google.com/search?q=%23question-5-finding-broadcast-address--usable-range)**

---

### 🔍 Solution for Question 5

#### Answer:

1. **Subnet Mask:** `255.255.255.224`
2. **Network ID:** `192.168.1.128`
3. **Broadcast Address:** `192.168.1.159`
4. **Usable Host Range:** `192.168.1.129` to `192.168.1.158`

#### Step-by-Step Explanation:

1. **Find Subnet Mask:**
* `/27` means 27 `1`s: $8 + 8 + 8 + 3 = 27$.
* The 4th octet has 3 bits turned on (`11100000`): $128 + 64 + 32 = \mathbf{224}$.
* Subnet Mask: **`255.255.255.224`**.


2. **Calculate Block Size:**

$$\text{Block Size} = 256 - 224 = \mathbf{32}$$


3. **Find Subnet Boundaries (Counting by 32 in the 4th octet):**
* `.0`, `.32`, `.64`, `.96`, **`.128`**, `.160`...
* The IP `.138` falls between `.128` and `.159`.


4. **Identify Range Components:**
* **Network ID:** `192.168.1.128` (first address)
* **First Usable IP:** `192.168.1.129`
* **Last Usable IP:** `192.168.1.158`
* **Broadcast Address:** `192.168.1.159` (one value before the next subnet `.160`)


↩️ **[Back to Question 5](https://www.google.com/search?q=%23question-5-finding-broadcast-address--usable-range)**

### 🔍 Solution for Question 6

#### Answer: `255.255.252.0`

#### Step-by-Step Explanation:

1. **Understand CIDR:** A `/22` prefix means the first 22 bits out of 32 are set to `1`.
2. **Break down into 4 octets (8 bits each):**
* 1st Octet: 8 bits = `11111111` ($255$)
* 2nd Octet: 8 bits = `11111111` ($255$)
* 3rd Octet: 6 bits = `11111100` ($128 + 64 + 32 + 16 + 8 + 4 = 252$)
* 4th Octet: 0 bits = `00000000` ($0$)



$$\text{Subnet Mask: } \mathbf{255.255.252.0}$$

↩️ **[Back to Question 6](https://www.google.com/search?q=%23question-6-cidr-prefix-to-subnet-mask-conversion)** | ➡️ **[Go to Question 7](https://www.google.com/search?q=%23question-7-subnet-range-in-the-3rd-octet)**

---

### 🔍 Solution for Question 7

#### Answer:

1. **Subnet Mask:** `255.255.224.0`
2. **Network ID:** `10.20.128.0`
3. **Broadcast Address:** `10.20.159.255`

#### Step-by-Step Explanation:

1. **Find the Subnet Mask:**
* `/19` means 19 bits set to `1` ($8 + 8 + 3 = 19$).
* The 3rd octet has 3 bits turned on (`11100000`): $128 + 64 + 32 = \mathbf{224}$.
* Subnet Mask: **`255.255.224.0`**.


2. **Calculate Block Size:**
* The **Interesting Octet** is the 3rd octet (`224`).
* $\text{Block Size} = 256 - 224 = \mathbf{32}$.


3. **Find Subnet Boundaries (Counting by 32 in the 3rd octet):**
* `.0.0`, `.32.0`, `.64.0`, `.96.0`, **`.128.0`**, `.160.0`...
* The IP's 3rd octet value is `130`, which falls between `128` and `159`.


4. **Identify Range Components:**
* **Network ID:** `10.20.128.0`
* **Broadcast Address:** `10.20.159.255` (one value before `10.20.160.0`)



↩️ **[Back to Question 7](https://www.google.com/search?q=%23question-7-subnet-range-in-the-3rd-octet)** | ➡️ **[Go to Question 8](https://www.google.com/search?q=%23question-8-wildcard-mask-calculation)**

---

### 🔍 Solution for Question 8

#### Answer: `0.0.63.255`

#### Step-by-Step Explanation:

1. **Determine the Subnet Mask for `/18`:**
* $8 + 8 + 2 = 18$ bits $\rightarrow$ 3rd octet has 2 bits on (`11000000` = $192$).
* Subnet Mask: `255.255.192.0`.


2. **Calculate the Wildcard Mask:**
* Subtract the Subnet Mask from `255.255.255.255`:


```text
  255 . 255 . 255 . 255
- 255 . 255 . 192 .   0
-----------------------
    0 .   0 .  63 . 255

```



$$\text{Wildcard Mask: } \mathbf{0.0.63.255}$$

↩️ **[Back to Question 8](https://www.google.com/search?q=%23question-8-wildcard-mask-calculation)** | ➡️ **[Go to Question 9](https://www.google.com/search?q=%23question-9-same-subnet-verification)**

---

### 🔍 Solution for Question 9

#### Answer:

**No**, Host A cannot communicate directly with Host B without a Layer 3 router because they reside in **different subnets**.

#### Step-by-Step Explanation:

1. **Analyze Mask `/26` (`255.255.255.192`):**
* $\text{Block Size} = 256 - 192 = \mathbf{64}$.
* Subnets increment by 64 in the 4th octet:
* Subnet 1: `192.168.1.0 /26` (Range: `.0` to `.63`)
* Subnet 2: `192.168.1.64 /26` (Range: `.64` to `.127`)
* Subnet 3: `192.168.1.128 /26` (Range: `.128` to `.191`)




2. **Locate Each Host:**
* **Host A (`192.168.1.67`):** Belongs to **Subnet 2** (`192.168.1.64 /26`).
* **Host B (`192.168.1.130`):** Belongs to **Subnet 3** (`192.168.1.128 /26`).


3. **Conclusion:** Since Host A and Host B have different Network IDs, their traffic must be routed by a default gateway (router or Layer 3 switch).

↩️ **[Back to Question 9](https://www.google.com/search?q=%23question-9-same-subnet-verification)** | ➡️ **[Go to Question 10](https://www.google.com/search?q=%23question-10-designing-a-subnet-for-a-specific-host-requirement)**

---

### 🔍 Solution for Question 10

#### Answer:

1. **Prefix Length:** `/27`
2. **Block Size:** `32`
3. **Network ID of 2nd Subnet:** `192.168.50.32`

#### Step-by-Step Explanation:

1. **Find Required Host Bits ($h$):**
* Formula: $2^h - 2 \ge 28$
* $h = 4$ bits $\rightarrow 2^4 - 2 = 14$ hosts (Too small)
* $h = 5$ bits $\rightarrow 2^5 - 2 = 30$ hosts (Meets the 28-host requirement efficiently!)


2. **Calculate Prefix Length:**
* $\text{Prefix} = 32 - 5 = \mathbf{/27}$ (`255.255.255.224`).


3. **Calculate Block Size:**
* $\text{Block Size} = 256 - 224 = \mathbf{32}$ (or $2^5 = 32$).


4. **Identify Subnet Boundaries:**
* 1st Subnet: `192.168.50.0 /27`
* 2nd Subnet: **`192.168.50.32 /27`**


↩️ **[Back to Question 10](https://www.google.com/search?q=%23question-10-designing-a-subnet-for-a-specific-host-requirement)**