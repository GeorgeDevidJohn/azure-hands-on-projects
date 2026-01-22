# 🔐 NetShield  
## ASG–NSG Driven Multi-Tier Security Architecture in Microsoft Azure

![Microsoft Azure](https://img.shields.io/badge/Microsoft-Azure-blue)
![Cloud Security](https://img.shields.io/badge/Domain-Cloud%20Security-critical)
![Linux](https://img.shields.io/badge/OS-Ubuntu-orange)
![Status](https://img.shields.io/badge/Project-Completed-success)

---

## 📘 Introduction
Modern cloud applications are deployed across multiple tiers such as **Web**, **Application**, and **Database**, each requiring strict access control. Poor network segmentation can lead to unauthorized access and lateral movement attacks.

**NetShield** is a practical Microsoft Azure project that demonstrates how to build a **secure, enterprise-grade three-tier architecture** using **Network Security Groups (NSGs)** and **Application Security Groups (ASGs)**. The project focuses on **defense in depth**, **controlled traffic flow**, and **monitoring with alerts**.

---

## 🎯 Objectives
- Design a secure three-tier Azure architecture  
- Implement Azure Virtual Networks and subnets  
- Configure Network Security Groups (NSGs)  
- Use Application Security Groups (ASGs) for scalable security  
- Validate rules using real VM traffic  
- Implement Azure Monitor alerts  
- Analyze logs and performance metrics  

---

## 🏗️ Architecture

### Components
- Resource Group  
- Virtual Network (VNET)  
- Subnets: Web, App, Database  
- Ubuntu Virtual Machines  
- Network Security Groups (NSG)  
- Application Security Groups (ASG)  
- Azure Monitor & Alerts  

### Traffic Rules

| Source | Destination | Access | Reason |
|------|------------|--------|--------|
| Web VM | App VM | Allowed | Application communication |
| Web VM | DB VM | Denied | Prevent direct DB access |
| App VM | DB VM | Allowed | Backend access |
| Any VM | Internet | Controlled | Security best practice |

---

## ⚙️ Implementation

### 1. Resource Group
- **Name:** `project-2-rs`
- **Region:** Canada Central

---

### 2. Virtual Network
- **VNET:** `NetShield-VNET`
- **Address Space:** `10.0.0.0/16`

| Subnet | CIDR |
|------|------|
| web-subnet | 10.0.1.0/24 |
| app-subnet | 10.0.2.0/24 |
| db-subnet | 10.0.3.0/24 |

---

### 3. Virtual Machines

| VM | Subnet | Role |
|---|-------|------|
| web-vm | web-subnet | Frontend |
| app-vm | app-subnet | Application |
| db-vm | db-subnet | Database |

---

## 🔐 Network Security Groups (NSG)

- **NSG Name:** `NetShield-NSG`
- Allow Web → App  
- Deny Web → DB  

---

## 🧩 Application Security Groups (ASG)

- `ASG-Web`
- `ASG-App`

Allow TCP port **8080** from Web to App.

---

## 📊 Monitoring & Alerts

- CPU alert when usage exceeds **60%**
- Email notifications via Azure Monitor

---

## 🧠 Skills Gained
- Azure Virtual Networking  
- Network Security Groups (NSG)  
- Application Security Groups (ASG)  
- Secure Cloud Architecture  
- Linux VM Administration  
- Azure Monitor & Alerts  

---

## 📐 Architecture Diagram
_Add diagram image here_
