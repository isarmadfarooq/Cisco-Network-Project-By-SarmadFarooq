# Vic Modern Hotel Network Infrastructure Project

## 📘 Project Summary

As part of my final year networking project, I successfully designed and implemented a comprehensive, scalable, and secure network infrastructure for **Vic Modern Hotel**, a multi-floor hospitality environment. The network was developed to support interdepartmental communication, wireless access, secure remote management, and dynamic IP allocation using enterprise-level configurations.

---

## 🏨 Hotel Overview

Vic Modern Hotel is structured into **three floors**, each containing specific departments:

- **1st Floor:** Reception, Store, Logistics  
- **2nd Floor:** Finance, HR, Sales/Marketing  
- **3rd Floor:** IT, Admin  

Each department is logically segmented using **VLANs**, connected through managed switches and routed via routers placed centrally in the **IT Department's server room**.

---

## 📡 Network Topology Design

### 🔗 Core Router Connectivity

- **Three Routers** installed in the server room of the IT department (one per floor).
- Routers are connected **via Serial DCE links** using the following IP scheme:
  - Router1 ↔ Router2: `10.10.10.0/30`
  - Router2 ↔ Router3: `10.10.10.4/30`
  - Router1 ↔ Router3: `10.10.10.8/30`

### 🔌 Switch and Access Layer Setup

- **Three managed switches** (one per floor).
- **Trunk ports** configured between router and switch (Router-on-a-Stick).
- Each department assigned a dedicated VLAN and subnet.

---

## 📁 VLAN & IP Schema

| Floor       | Department       | VLAN ID | Subnet            |
|-------------|------------------|---------|-------------------|
| 1st Floor   | Reception         | 80      | 192.168.8.0/24    |
|             | Store             | 70      | 192.168.7.0/24    |
|             | Logistics         | 60      | 192.168.6.0/24    |
| 2nd Floor   | Finance           | 50      | 192.168.5.0/24    |
|             | HR                | 40      | 192.168.4.0/24    |
|             | Sales/Marketing   | 30      | 192.168.3.0/24    |
| 3rd Floor   | Admin             | 20      | 192.168.2.0/24    |
|             | IT                | 10      | 192.168.1.0/24    |

Each department is isolated in its own VLAN for security and broadcast management.

---

## 🔧 What I Did (Implementation Breakdown)

### ✅ Routing & OSPF Configuration
- Implemented **OSPF (Open Shortest Path First)** protocol on all routers using Process ID `1`.
- Advertised all internal VLAN networks and serial interfaces for full inter-VLAN and inter-floor communication.

### ✅ VLAN & Trunk Configuration
- Created VLANs on switches with proper **VLAN IDs** and **interface assignments**.
- Configured **sub-interfaces on routers** for each VLAN (Router-on-a-Stick).
- Enabled trunking on switch-router interfaces to allow multiple VLAN traffic.

### ✅ Dynamic IP Addressing (DHCP)
- Each router was configured as a **DHCP server** for its local VLANs.
- Configured `ip dhcp excluded-address` to reserve key IPs.
- Ensured **laptops, phones, and printers** obtain IP addresses dynamically in their respective VLAN subnets.

### ✅ Wireless Connectivity
- Simulated wireless networks for each floor.
- Connected laptops and smartphones wirelessly with DHCP-enabled IPs.

### ✅ Device Deployment
- Installed one **printer per department**, configured with DHCP.
- Verified that printers and user devices can communicate within and across VLANs using routing.

### ✅ SSH Secure Access
- Configured **SSH on all routers** for secure remote login.
- Created local user credentials and domain configuration for encryption.
- Verified login using a test machine.

### ✅ Port Security
- On the **IT Department switch**, configured **port Fa0/1** for the **Test-PC**:
  - Used **sticky MAC address learning**.
  - Applied **violation mode "shutdown"** to secure the port from unauthorized access.

### ✅ Final Testing and Validation
- Verified **ping and SSH access** from `Test-PC` to all routers.
- Ensured **inter-VLAN communication** works as intended.
- Tested **DHCP address allocation** across all departments.
- Triggered port security violations to test switch lockdown behavior.

---

## 🔐 Security Measures Implemented

- **SSH-enabled routers** to avoid plaintext remote access.
- **MAC address sticky binding** and **violation shutdown mode** for unauthorized device mitigation.
- Logical segmentation of network using **VLANs** to isolate department traffic.

---

## 🛠 Tools & Technologies Used

- **Cisco Packet Tracer** (Network Simulation)
- **Cisco IOS Commands** for Routing, VLAN, DHCP, SSH, and Port Security
- Layer 2/3 Network Concepts: Trunking, Sub-interfaces, Routing Protocols, DHCP
- Network Testing Tools: `ping`, `ssh`, interface status checks

---

## 👨‍💻 Author

**Sarmad Farooq**  
Final Year Computer Science Student – UET Lahore  
Specializing in Network Design, Cybersecurity, and Systems Administration  
Email: [you@example.com]  
LinkedIn: [linkedin.com/in/sarmad-farooq](https://www.linkedin.com/in/sarmad-farooq)

---

## 📌 Conclusion

This project demonstrates real-world skills in designing and implementing scalable enterprise networks using VLANs, OSPF, DHCP, wireless networking, and remote management with a focus on security and performance. The setup ensures all departments are logically isolated yet fully connected across the hotel infrastructure.

<img width="908" alt="3rd_projet_Hotel_Management_System_Diagram" src="https://github.com/user-attachments/assets/606a1670-3f4e-4219-a5b5-aff59ea42144" />
