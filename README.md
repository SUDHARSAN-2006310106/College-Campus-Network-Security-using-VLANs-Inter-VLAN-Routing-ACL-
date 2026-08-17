
# 🔐 College Campus Network Security Using VLANs, Inter-VLAN Routing & ACL

![Cisco](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?logo=cisco\&logoColor=white)
![Networking](https://img.shields.io/badge/Domain-Computer%20Networking-blue)
![VLAN](https://img.shields.io/badge/Technology-VLAN-green)
![Security](https://img.shields.io/badge/Security-ACL-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📌 Project Overview

This project demonstrates the design and implementation of a **secure college campus network** using **Cisco Packet Tracer**.

The network is logically segmented into multiple VLANs based on different departments. **Inter-VLAN Routing** enables controlled communication between VLANs, while **Access Control Lists (ACLs)** are implemented to restrict unauthorized access between departments.

The project focuses on improving **network segmentation, communication, security, scalability, and manageability** in a campus network environment.

---

## 🎯 Objectives

* Design a structured college campus network.
* Divide departments into separate VLANs.
* Implement VLAN-based network segmentation.
* Configure trunk links between switches.
* Enable communication between VLANs using Inter-VLAN Routing.
* Implement ACLs to control traffic between departments.
* Configure DHCP for automatic IP address assignment.
* Improve network security using Cisco networking features.
* Test and verify authorized and unauthorized communication.

---

## 🏫 Network Architecture

The campus network consists of multiple departments:

```text
                         ┌─────────────────┐
                         │    Internet     │
                         └────────┬────────┘
                                  │
                             ┌────▼────┐
                             │ Router  │
                             └────┬────┘
                                  │
                         ┌────────▼────────┐
                         │  Core Switch    │
                         └───────┬─────────┘
                                 │
              ┌──────────────────┼──────────────────┐
              │                  │                  │
        ┌─────▼─────┐      ┌─────▼─────┐      ┌─────▼─────┐
        │   Admin   │      │  Faculty  │      │  Students │
        │   VLAN 10 │      │   VLAN 20 │      │   VLAN 30 │
        └───────────┘      └───────────┘      └───────────┘
                                 │
                          ┌──────▼──────┐
                          │     Lab     │
                          │   VLAN 40   │
                          └─────────────┘
```

> **Note:** Replace the topology above with your actual Packet Tracer topology screenshot in the repository.

---

## 🧩 VLAN Configuration

| VLAN ID | Department     | Network         | Purpose                |
| ------: | -------------- | --------------- | ---------------------- |
|      10 | Administration | 192.168.10.0/24 | Administrative systems |
|      20 | Faculty        | 192.168.20.0/24 | Faculty systems        |
|      30 | Students       | 192.168.30.0/24 | Student systems        |
|      40 | Computer Lab   | 192.168.40.0/24 | Laboratory systems     |
|      50 | Management     | 192.168.50.0/24 | Network management     |

---

## 🌐 IP Addressing Scheme

| VLAN | Network Address | Default Gateway | Subnet Mask   |
| ---: | --------------- | --------------- | ------------- |
|   10 | 192.168.10.0/24 | 192.168.10.1    | 255.255.255.0 |
|   20 | 192.168.20.0/24 | 192.168.20.1    | 255.255.255.0 |
|   30 | 192.168.30.0/24 | 192.168.30.1    | 255.255.255.0 |
|   40 | 192.168.40.0/24 | 192.168.40.1    | 255.255.255.0 |
|   50 | 192.168.50.0/24 | 192.168.50.1    | 255.255.255.0 |

---

# 🔧 Technologies & Concepts Used

* Cisco Packet Tracer
* VLAN
* Inter-VLAN Routing
* Access Control Lists (ACL)
* DHCP
* Trunking
* Access Ports
* IP Addressing
* Subnetting
* Routing
* Network Security
* Cisco IOS Commands

---

# 🔐 Network Security Design

The network uses ACLs to control communication between departments.

### Example Security Policy

| Source         | Destination     | Access  |
| -------------- | --------------- | ------- |
| Students       | Student Lab     | ✅ Allow |
| Students       | Faculty         | ❌ Deny  |
| Students       | Administration  | ❌ Deny  |
| Faculty        | Administration  | ✅ Allow |
| Faculty        | Students        | ✅ Allow |
| Administration | All Departments | ✅ Allow |
| Management     | Network Devices | ✅ Allow |

This approach prevents unauthorized users from accessing sensitive departmental resources.

---

# 🔀 Inter-VLAN Routing

Since different VLANs represent different logical networks, communication between them requires Layer 3 routing.

The project implements **Inter-VLAN Routing** so that authorized devices can communicate across VLAN boundaries.

Example:

```text
Student PC
192.168.30.10
      │
      ▼
   VLAN 30
      │
      ▼
Inter-VLAN Routing
      │
      ▼
   VLAN 20
      │
      ▼
Faculty PC
192.168.20.10
```

ACL rules are then used to determine whether the communication should be allowed or denied.

---

# 🛡️ ACL Configuration

ACLs are used to filter network traffic according to security requirements.

Example:

```cisco
access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.20.0 0.0.0.255
access-list 100 permit ip any any
```

### Explanation

The ACL:

1. Blocks Student VLAN traffic to Administration.
2. Blocks Student VLAN traffic to Faculty.
3. Allows other permitted traffic.

> Adjust the ACL commands according to your actual Packet Tracer configuration.

---

# 📡 DHCP Configuration

DHCP is used to automatically assign IP addresses to end devices.

Example:

```cisco
ip dhcp pool STUDENTS
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 8.8.8.8
```

This reduces manual IP configuration and makes network management easier.

---

# 🧪 Network Testing

The network was tested using different connectivity scenarios.

### Test 1 — Same VLAN Communication

```text
Student PC → Student PC
Result: ✅ Successful
```

### Test 2 — Authorized Inter-VLAN Communication

```text
Faculty → Administration
Result: ✅ Successful
```

### Test 3 — Unauthorized Access

```text
Student → Administration
Result: ❌ Blocked by ACL
```

### Test 4 — Student to Faculty

```text
Student → Faculty
Result: ❌ Blocked by ACL
```

### Test 5 — DHCP

```text
End Device → DHCP Server/Router
Result: ✅ IP Address Assigned
```

---

# 📊 Verification Commands

The following Cisco IOS commands were used to verify the network configuration:

```cisco
show vlan brief
```

```cisco
show interfaces trunk
```

```cisco
show ip interface brief
```

```cisco
show access-lists
```

```cisco
show ip route
```

```cisco
show running-config
```

---

# 📁 Project Structure

```text
College-Campus-Network-Security/
│
├── README.md
│
├── College_Campus_Network.pkt
│
├── Configurations/
│   ├── Router.txt
│   ├── Core_Switch.txt
│   ├── Admin_Switch.txt
│   ├── Faculty_Switch.txt
│   └── Student_Switch.txt
│
├── Documentation/
│   ├── IP_Addressing_Table.pdf
│   └── Network_Configuration.pdf
│
└── Screenshots/
    ├── Final_Topology.png
    ├── VLAN_Configuration.png
    ├── InterVLAN_Routing.png
    ├── ACL_Configuration.png
    └── Ping_Test.png

# 🚀 Key Features

* ✅ Department-wise VLAN segmentation
* ✅ Inter-VLAN communication
* ✅ ACL-based traffic filtering
* ✅ DHCP configuration
* ✅ Trunk and access port configuration
* ✅ IP addressing and subnetting
* ✅ Network connectivity testing
* ✅ Basic campus network security
* ✅ Cisco IOS configuration and troubleshooting

---

