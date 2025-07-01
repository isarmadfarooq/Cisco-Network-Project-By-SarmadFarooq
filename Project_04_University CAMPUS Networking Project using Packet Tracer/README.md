Here's a complete `README.md` file tailored for your Albion University Cisco Packet Tracer project, covering **network planning**, **configuration**, and **brief explanations** of all steps and components involved.

---

```markdown
# Albion University Network Design & Configuration Project

## Author: Sarmad Farooq  
## Tool: Cisco Packet Tracer  
## Project: University Network Topology and Configuration  
## Course: Networking / CCNA Coursework  
## Date: [Insert your submission date]

---

## 📌 Overview

This project involves the **planning**, **design**, and **implementation** of a network for **Albion University**, which operates across **two campuses**. The goal is to ensure proper communication between departments, isolated traffic via VLANs, dynamic IP assignment, and access to internal and external servers using RIPv2 and static routing.

---

## 🏫 Network Architecture Summary

### ✅ Main Campus (3 Buildings)
- **Building A**: Administrative Departments (Management, HR, Finance) + Faculty of Business  
- **Building B**: Faculty of Engineering/Computing + Faculty of Art and Design  
- **Building C**: Students' Labs + IT Department (Hosts Web Server, DNS, FTP etc.)

### ✅ Smaller Campus
- **Faculty of Health and Sciences**  
  - Staff on one floor  
  - Students on another floor  

### ✅ External Services
- Cloud-hosted Email Server (Static IP configuration)

---

## ⚙️ Configuration & Topology Plan

### 1️⃣ VLAN Planning (on Switches)
Each department/faculty is mapped to a unique VLAN:
| VLAN Name         | VLAN ID | Department                     |
|-------------------|---------|--------------------------------|
| VLAN_Admin_HR     | 10      | HR                              |
| VLAN_Admin_MGMT   | 20      | Management                     |
| VLAN_Admin_Fin    | 30      | Finance                        |
| VLAN_Business     | 40      | Business Faculty               |
| VLAN_EngComp      | 50      | Engineering & Computing        |
| VLAN_ArtDesign    | 60      | Art & Design                   |
| VLAN_Labs         | 70      | Student Labs                   |
| VLAN_IT           | 80      | IT Department (Server Access)  |
| VLAN_Health_Staff | 90      | Health Faculty (Staff)         |
| VLAN_Health_Std   | 100     | Health Faculty (Students)      |

### 2️⃣ IP Addressing Plan
- **10.0.x.0/24** per department (x = VLAN ID)
- **Dynamic IPs via DHCP** for Building A using Router DHCP
- **Static IPs** for servers and routers

Example:
```

VLAN 10 - HR:           10.0.10.0/24
VLAN 20 - Management:   10.0.20.0/24
VLAN 30 - Finance:      10.0.30.0/24
...
VLAN 80 - IT Dept:      10.0.80.0/24 (Servers)

````

### 3️⃣ Routing Protocol
- **RIPv2** between internal routers for dynamic routing
- **Static route** to the external email server (e.g. 200.10.10.5/32)

### 4️⃣ DHCP Setup (Router in Building A)
```bash
ip dhcp pool HR
   network 10.0.10.0 255.255.255.0
   default-router 10.0.10.1

ip dhcp pool MGMT
   network 10.0.20.0 255.255.255.0
   default-router 10.0.20.1

! And so on for all VLANs in Building A
````

### 5️⃣ Switch VLAN Configuration

```bash
vlan 10
 name HR
vlan 20
 name MGMT
...

interface fa0/1
 switchport mode access
 switchport access vlan 10

interface fa0/24
 switchport mode trunk
```

### 6️⃣ Router-on-a-Stick Setup (Inter-VLAN Routing)

```bash
interface g0/0.10
 encapsulation dot1Q 10
 ip address 10.0.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 10.0.20.1 255.255.255.0
...
```

### 7️⃣ RIP Configuration

```bash
router rip
 version 2
 no auto-summary
 network 10.0.0.0
```

### 8️⃣ Static Route for External Email Server

```bash
ip route 200.10.10.5 255.255.255.255 192.168.1.1
```

---

## 🧪 Testing & Verification

| Test                 | Command                          | Result |
| -------------------- | -------------------------------- | ------ |
| VLAN Connectivity    | `ping` between same VLAN devices | ✅      |
| Inter-VLAN Routing   | `ping` across VLANs              | ✅      |
| DHCP Allocation      | `ipconfig` on clients            | ✅      |
| RIP Neighbors        | `show ip route`                  | ✅      |
| Server Access        | Browser or `ping`                | ✅      |
| External Mail Server | `ping 200.10.10.5`               | ✅      |

---

## 🔒 Security Settings

* Disabled unused switch ports:

```bash
interface range fa0/10 - 24
 shutdown
```

* Enabled port-security for endpoint ports:

```bash
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation restrict
```

---

## 🛠️ Troubleshooting Steps Taken

* **Issue**: PCs not getting IPs
  **Fix**: Ensured trunk port between switch and router and VLAN interfaces were configured properly.

* **Issue**: No internet/external access
  **Fix**: Configured static route and default gateway.

* **Issue**: VLANs not communicating
  **Fix**: Verified router subinterfaces and trunk ports on switches.

---

## 🖼️ Topology Snapshot

> (Attach a screenshot of your Cisco Packet Tracer topology here)

---

## 📚 Conclusion

This project demonstrated a structured approach to **network planning**, **VLAN segmentation**, **inter-VLAN routing**, **DHCP**, **server access**, and **external routing**. Cisco Packet Tracer was used to simulate a real-world scalable and secure campus network with multiple departments and servers.

---

## 🔗 Additional Notes

* Cloud server (email) was simulated using a PC with static IP
* Server IPs were reserved manually to avoid DHCP conflicts
* Used labels and naming conventions for clarity in Packet Tracer

<img width="924" alt="University CAMPUS Networking Project using Packet Tracer Diagram" src="https://github.com/user-attachments/assets/7daa4a8a-925c-467c-beb8-584ada45ce0e" />
