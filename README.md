# VLAN-Segmentation
Learning VLANs the practical way! Step-by-step guides and Packet Tracer projects showing how to segment networks, secure devices, and manage traffic like a pro.

VLAN stands for Virtual Local Area Network. It is a method of logically segmenting a physical network into multiple broadcast domains. This means you can group devices together—even if they're not physically connected to the same switch—so they behave like they're on the same local network. In simpler terms, VLANs allow you to divide a single switch into multiple smaller "virtual" switches, helping organize your network better.

🛠️ Why Do We Use VLANs?
Here are the main reasons for using VLANs:

1. 🔐 Improved Security
Devices in different VLANs cannot communicate with each other directly without a Layer 3 device (like a router). This limits access between departments or user groups (e.g., HR and IT), reducing the attack surface.

✅ Example: HR computers and Guest Wi-Fi users are separated into different VLANs to prevent unauthorized access to sensitive data.

2. 📊 Better Network Performance
By creating VLANs, you reduce unnecessary broadcast traffic. Each VLAN becomes its own broadcast domain, which keeps traffic localized.

✅ Example: Instead of sending all broadcast packets across the whole network, each VLAN only sends them to relevant members.

3. 🧩 Simplified Network Management
You can organize devices based on function, department, or user role, not just physical location.

✅ Example: All IT devices can be in VLAN 20, even if they’re located on different floors or switches.

4. 🌍 Logical Grouping of Devices
VLANs make it easier to group and manage devices logically, such as printers, VoIP phones, or servers—even if they’re spread across different switches or locations.

5. 📈 Scalability
VLANs make your network more scalable and adaptable. You can move a user to a different part of the building and still keep them in the same VLAN without physically rewiring anything.

# 🌐 VLAN Segmentation with Cisco Packet Tracer

This project demonstrates how to implement VLAN segmentation using Cisco Packet Tracer. It includes complete configuration steps, IP planning, and inter-VLAN routing setup to simulate a secure and organized enterprise network.

---

## 📘 What is a VLAN?

A **VLAN (Virtual Local Area Network)** is a method of logically segmenting a network into separate broadcast domains. VLANs allow you to group devices based on function, department, or access level — not physical location — improving both performance and security.

---

## ✅ Why Use VLANs?

- 🔐 **Security**: Restrict communication between departments (e.g., HR vs. IT)
- 📊 **Performance**: Reduce broadcast traffic by isolating domains
- ⚙️ **Manageability**: Group devices logically across locations
- 📈 **Scalability**: Easily add users or devices without rewiring
- 🌍 **Flexibility**: Move users without reconfiguring the physical network

---


## 🏗️ Project Topology

PC1 (HR) PC2 (IT) PC3 (SALES)
| | |
Switch S1 ---------------- Switch S2
| | |
PC4 (HR) PC5 (IT) PC6 (SALES)
|
Router (R1)

![image](https://github.com/user-attachments/assets/24535a5b-4edb-4677-ac66-603a4ded4365)



- VLAN 10: HR – 192.168.10.0/24  
- VLAN 20: IT – 192.168.20.0/24  
- VLAN 30: SALES – 192.168.30.0/24

---

## 🛠️ Devices Used

- 2 × Cisco 2960 Switches  
- 1 × Cisco Router (2911 or similar)  
- 6 × PCs  
- Cisco Packet Tracer

---

## 🔧 Configuration Steps

### Step 1: Assign VLANs
```bash
vlan 10
 name HR
vlan 20
 name IT
vlan 30
 name SALES


- VLAN 10: HR – 192.168.10.0/24  
- VLAN 20: IT – 192.168.20.0/24  
- VLAN 30: SALES – 192.168.30.0/24

---

## 🛠️ Devices Used

- 2 × Cisco 2960 Switches  
- 1 × Cisco Router (2911 or similar)  
- 6 × PCs  
- Cisco Packet Tracer

---

## 🔧 Configuration Steps

### Step 1: Assign VLANs
```bash
vlan 10
 name HR
vlan 20
 name IT
vlan 30
 name SALES

Step 2: Assign Ports to VLANs
interface fa0/1
 switchport mode access
 switchport access vlan 10
(Repeat for each port and VLAN)

Step 3: Configure Trunk Links
interface fa0/24
 switchport mode trunk

Step 4: Router-on-a-Stick Setup
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0

interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0

Step 5: Test Connectivity
Ping devices within the same VLAN ✅

Ping across VLANs to confirm inter-VLAN routing ✅

