# VLAN-Segmentation
Learning VLANs the practical way! Step-by-step guides and Packet Tracer projects showing how to segment networks, secure devices, and manage traffic like a pro.

VLAN stands for Virtual Local Area Network. It is a method of logically segmenting a physical network into multiple broadcast domains. This means you can group devices together—even if they're not physically connected to the same switch—so they behave like they're on the same local network. In simpler terms, VLANs allow you to divide a single switch into multiple smaller "virtual" switches, helping organize your network better.

🎯 Why We Use VLAN?
Segmentation: Isolates traffic for better performance.

Security: Users in one VLAN cannot communicate with another without a router.

Flexibility: Devices can be grouped based on function, not physical location.

Traffic Control: Reduces unnecessary broadcast traffic.


This project demonstrates how to implement VLAN segmentation using Cisco Packet Tracer. It includes complete configuration steps, IP planning, and inter-VLAN routing setup to simulate a secure and organized enterprise network.

---

## 📘 What is a VLAN?

A **VLAN (Virtual Local Area Network)** is a method of logically segmenting a network into separate broadcast domains. VLANs allow you to group devices based on function, department, or access level — not physical location — improving both performance and security.

🌐 Project Topology
Router: Router0

Switch: Switch0

PCs: PC1 to PC6

VLANs:

VLAN 10 – HR (PC1, PC2)

VLAN 20 – Finance (PC3, PC4)

VLAN 30 – IT (PC5, PC6)

🛠️ Step-by-Step Configuration
✅ Step 1: Assign Devices in Packet Tracer
Drag and drop 1 router (e.g., 2911), 1 switch (2960), and 6 PCs.

Connect all 6 PCs to the switch using Copper Straight-Through cables.

Connect Switch to Router’s G0/0 port using Copper Straight-Through.

✅ Step 2: Configure VLANs on the Switch
Click on the Switch > CLI and enter:

bash
Copy
Edit
enable
configure terminal
vlan 10
name HR
exit
vlan 20
name Finance
exit
vlan 30
name IT
exit
✅ Step 3: Assign Ports to VLANs
Let’s assume:

PC1 → Fa0/1 and PC2 → Fa0/2 (VLAN 10)

PC3 → Fa0/3 and PC4 → Fa0/4 (VLAN 20)

PC5 → Fa0/5 and PC6 → Fa0/6 (VLAN 30)

bash
Copy
Edit
interface range fa0/1 - 2
switchport mode access
switchport access vlan 10
exit

interface range fa0/3 - 4
switchport mode access
switchport access vlan 20
exit

interface range fa0/5 - 6
switchport mode access
switchport access vlan 30
exit
✅ Step 4: Configure Trunk Port for Router
Assume Switch Port Fa0/24 → Router G0/0:

bash
Copy
Edit
interface fa0/24
switchport trunk encapsulation dot1q
switchport mode trunk
exit
✅ Step 5: Configure Router Sub-Interfaces
Click Router > CLI:

bash
Copy
Edit
enable
configure terminal
interface g0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0
exit

interface g0/0.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0
exit

interface g0/0.30
encapsulation dot1q 30
ip address 192.168.30.1 255.255.255.0
exit

interface g0/0
no shutdown
exit
✅ Step 6: Assign IP Addresses to PCs
PC1 & PC2 (VLAN 10):

IP: 192.168.10.2 / 192.168.10.3

Gateway: 192.168.10.1

PC3 & PC4 (VLAN 20):

IP: 192.168.20.2 / 192.168.20.3

Gateway: 192.168.20.1

PC5 & PC6 (VLAN 30):

IP: 192.168.30.2 / 192.168.30.3

Gateway: 192.168.30.1

✅ Step 7: Save Configurations (Optional but Good Practice)
On Switch & Router:

bash
Copy
Edit
copy running-config startup-config
✅ Step 8: Testing
From PC1 (HR) try to ping PC3 (Finance) → Should work due to inter-VLAN routing.

Ping from PC5 (IT) to PC2 (HR) → Should work.

Use ping command in Command Prompt on the PCs.

📸 Screenshots for GitHub
Take these screenshots:

Topology diagram in Packet Tracer.

Switch VLAN Configuration.

Router Sub-Interface Configuration.

IP Configuration of one PC from each VLAN.

Successful Ping Tests.

Here is your complete README.md for the VLAN Segmentation and Inter-VLAN Routing Project — ready to upload to GitHub:

# VLAN Segmentation and Inter-VLAN Routing Project

This project demonstrates how to implement **VLAN Segmentation** and **Inter-VLAN Routing** using Cisco Packet Tracer with just:

- 🖥️ 1 Router (with sub-interfaces)
- 🔀 1 Switch
- 💻 6 PCs
- 🌐 3 VLANs

---

## 📘 What is VLAN?

**VLAN (Virtual Local Area Network)** allows a network administrator to segment a network into logical broadcast domains. This increases security, improves network performance, and provides better management of devices regardless of physical location.

---

## 🎯 Why Use VLAN?

- ✅ **Segregate network traffic** for departments (HR, Finance, IT, etc.)
- ✅ **Improve performance** by limiting broadcast domains
- ✅ **Enhance security** between groups of users
- ✅ **Ease of management** and flexibility in assigning devices

---

## 🧱 Topology Overview

| Device   | Interface  | VLAN | IP Address       | Description |
|----------|------------|------|------------------|-------------|
| Router0  | G0/0.10     | 10   | 192.168.10.1     | HR Gateway  |
| Router0  | G0/0.20     | 20   | 192.168.20.1     | Finance Gateway |
| Router0  | G0/0.30     | 30   | 192.168.30.1     | IT Gateway |
| PC1, PC2 | Fa0/1-2     | 10   | 192.168.10.2-3   | HR PCs |
| PC3, PC4 | Fa0/3-4     | 20   | 192.168.20.2-3   | Finance PCs |
| PC5, PC6 | Fa0/5-6     | 30   | 192.168.30.2-3   | IT PCs |
| Switch0  | Fa0/24      | Trunk| N/A              | Trunk to Router |

---

## 🔧 Configuration Steps

### 1. **Create VLANs on Switch**

```bash
vlan 10
name HR
vlan 20
name Finance
vlan 30
name IT
2. Assign Switch Ports to VLANs
bash
Copy
Edit
interface range fa0/1 - 2
switchport mode access
switchport access vlan 10

interface range fa0/3 - 4
switchport mode access
switchport access vlan 20

interface range fa0/5 - 6
switchport mode access
switchport access vlan 30
3. Configure Trunk Port (Switch → Router)
bash
Copy
Edit
interface fa0/24
switchport trunk encapsulation dot1q
switchport mode trunk
4. Configure Router Sub-Interfaces
bash
Copy
Edit
interface g0/0.10
encapsulation dot1q 10
ip address 192.168.10.1 255.255.255.0

interface g0/0.20
encapsulation dot1q 20
ip address 192.168.20.1 255.255.255.0

interface g0/0.30
encapsulation dot1q 30
ip address 192.168.30.1 255.255.255.0
5. Configure IPs on PCs
Example for PC1 (HR):

IP: 192.168.10.2

Subnet: 255.255.255.0

Gateway: 192.168.10.1

Repeat accordingly for all other PCs.

🧪 Testing
Ping from PC1 (HR) to PC3 (Finance) — ✅ Success

Ping from PC5 (IT) to PC2 (HR) — ✅ Success

Ping from PC4 (Finance) to PC6 (IT) — ✅ Success

All devices can communicate across VLANs through the router's sub-interfaces.


📸 Screenshots
Include the following screenshots in this repo:

🖼️ topology.png – Complete Packet Tracer topology

🖼️ switch_vlan_config.png – VLAN configuration on switch
![image](https://github.com/user-attachments/assets/92202a75-bda1-4a91-90b2-47d1a7fe435d)
![image](https://github.com/user-attachments/assets/4c97de37-6e1e-4271-8aa2-57cfa270c072)

🖼️ router_subinterfaces.png – Router sub-interface setup

🖼️ pc_ip_settings.png – Example IP config on a PC

🖼️ ping_test.png – Successful ping between VLANs


💡 Conclusion
This project illustrates how VLANs can securely and efficiently segment a network and how inter-VLAN routing enables communication across VLANs. Using a single router with sub-interfaces, we simulate a small enterprise setup with HR, Finance, and IT departments.

