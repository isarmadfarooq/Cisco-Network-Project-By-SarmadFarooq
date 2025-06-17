**XYZ Branch Network Design Proposal**

**Overview:**
XYZ company is expanding its operations by opening a new branch in Bonalbo, Eastern Australia. As the appointed network engineer, the goal is to design a small yet efficient and scalable network that operates independently from the HQ. The design must accommodate the company's departmental structure, promote communication, ensure secure access, and use a single router and switch (Cisco products).

**Network Requirements:**

1. **Hardware:**

   * 1 Cisco Router
   * 1 Cisco Switch

2. **Departments:**

   * Admin/IT
   * Finance/HR
   * Customer Service/Reception

3. **Subnetting and VLAN Design:**

   * Base Network: `192.168.1.0/24`
   * VLAN 10: Admin/IT (e.g., `192.168.1.0/26`)
   * VLAN 20: Finance/HR (e.g., `192.168.1.64/26`)
   * VLAN 30: Customer Service/Reception (e.g., `192.168.1.128/26`)
   * VLAN 99: Management VLAN (e.g., `192.168.1.192/28`)

4. **Services:**

   * **DHCP**: Router will assign IP addresses dynamically using DHCP for each VLAN
   * **Inter-VLAN Routing**: Enabled on the router using Router-on-a-Stick configuration
   * **Wireless Access**: Wireless Access Points (WAPs) will be connected for each department to support mobile users

5. **Connectivity Goals:**

   * Devices from different VLANs must communicate with each other (via Inter-VLAN routing)
   * Host devices must receive IP automatically (via DHCP)
   * Secure wireless access per department

**Step-by-Step Implementation Plan:**

1. **Physical Setup:**

   * Connect all PCs to the switch ports.
   * Connect switch to router via one trunk port.
   * Configure Access Points in each department.

2. **Router Configuration (Cisco CLI):**

```bash
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.192

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.65 255.255.255.192

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.1.129 255.255.255.192

interface GigabitEthernet0/0.99
 encapsulation dot1Q 99
 ip address 192.168.1.193 255.255.255.240

ip dhcp pool VLAN10
 network 192.168.1.0 255.255.255.192
 default-router 192.168.1.1

ip dhcp pool VLAN20
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.65

ip dhcp pool VLAN30
 network 192.168.1.128 255.255.255.192
 default-router 192.168.1.129
```

3. **Switch Configuration (Cisco CLI):**

```bash
vlan 10
 name Admin_IT
vlan 20
 name Finance_HR
vlan 30
 name Customer_Service
vlan 99
 name Management

interface range FastEthernet0/1 - 10
 switchport mode access
 switchport access vlan 10

interface range FastEthernet0/11 - 20
 switchport mode access
 switchport access vlan 20

interface range FastEthernet0/21 - 30
 switchport mode access
 switchport access vlan 30

interface GigabitEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
```

**Testing & Validation:**

* Ping between departments
* DHCP assignment verification
* Wireless connectivity testing per VLAN

**Conclusion:**
This network design ensures department-level segmentation via VLANs, DHCP-based IP distribution, inter-department communication via router-on-a-stick, and wireless access. The architecture is simple, cost-effective, and scalable for future branch upgrades.

**Next Steps:**

* Document and push configuration files to GitHub
* Diagram the network using draw\.io or Cisco Packet Tracer
* Perform testing in Packet Tracer or real devices
* Prepare for security hardening and monitoring
