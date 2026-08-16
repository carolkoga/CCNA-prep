# 📡 Cisco CCNA (200-301) Study Guide & Packet Tracer Labs

Welcome to my personal **Cisco CCNA (200-301)** study repository! 

This project began as my personal study guide and hands-on lab collection while preparing for the CCNA exam. Recognizing the value of structured, real-world practice, I opened this repository to the community to serve as a comprehensive theoretical and practical resource for anyone on their journey toward CCNA certification.

---

## 🎯 Repository Purpose

* **Comprehensive Command Cheatsheets:** Quick-reference syntax for Cisco IOS commands across all 3 NetAcad modules.
* **Hands-on Packet Tracer Labs (`.pkt`):** Practical network topologies designed to reinforce key networking concepts.
* **Step-by-Step Solutions:** Clear explanations and verification steps for every lab challenge.

---

## 🗺️ Course Structure & Modules

The repository is organized according to the Cisco Networking Academy (NetAcad) curriculum structure:

### [📂 Module 1: Introduction to Networks (ITN)](./module-1)
Focuses on fundamental networking concepts, the OSI and TCP/IP models, IP addressing (IPv4/IPv6), and baseline router/switch configuration.
* **Topics:** Initial Access, Console/VTY Security, SSH Setup, IPv4/IPv6 Interface Configuration, SVI Management, Diagnostics (`ping`/`traceroute`).
* **Guide:** [Read Module 1 Cheatsheet & Notes](./module-1/README.md)

### [📂 Module 2: Switching, Routing, and Wireless Essentials (SRWE)](./module-2)
Focuses on Layer 2 switching operations, VLAN segmentation, redundancy, and basic inter-VLAN routing.
* **Topics:** VLANs & 802.1Q Trunking, Spanning Tree Protocol (STP), EtherChannel (LACP), Inter-VLAN Routing (RoAS & SVI), DHCPv4, Port Security.
* **Guide:** [Read Module 2 Cheatsheet & Notes](./module-2/README.md)

### [📂 Module 3: Enterprise Networking, Security, and Automation (ENSA)](./module-3)
Focuses on large-scale enterprise network architecture, dynamic routing, WAN technologies, security controls, and modern automation.
* **Topics:** Single-Area OSPFv2, Standard & Extended ACLs, NAT/PAT, IPsec VPNs, Network Management (NTP, Syslog, SNMP), SDN & REST APIs.
* **Guide:** [Read Module 3 Cheatsheet & Notes](./module-3/README.md)

---

## 🧪 How to Use the Labs

1. Download and install **Cisco Packet Tracer** (v8.0 or newer recommended).
2. Navigate to the `/labs` directory inside any module folder.
3. Open a `.pkt` lab file:
   * **Unconfigured Labs:** Build and configure the topology from scratch following the instructions.
   * **Completed Labs:** Use as reference solutions to compare against your configurations.
4. Verify your work using the verification commands in each module's `README.md` or follow the step-by-step walkthroughs in the dedicated lab resolution documents.

---

## 🛠️ Prerequisites & Tools

* **Software:** Cisco Packet Tracer, VS Code (or Markdown editor of choice), Git.
* **Target Exam:** Cisco Certified Network Associate (CCNA 200-301).

---

## 🤝 Contributing & Feedback

Contributions, corrections, and improvements are welcome! If you spot an error in a command or want to add a useful Packet Tracer lab scenario:

1. Fork this repository.
2. Create a new branch (`git checkout -b feature/lab-fix`).
3. Commit your changes (`git commit -m 'Add new OSPF lab'`).
4. Push to the branch (`git push origin feature/lab-fix`).
5. Open a Pull Request.

---

⭐ **If you find this repository helpful for your CCNA prep, feel free to give it a star!**