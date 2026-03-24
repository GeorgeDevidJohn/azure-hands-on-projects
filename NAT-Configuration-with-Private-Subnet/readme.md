# 🌐 Azure Networking Project: NAT Configuration with Private Subnet

## 📌 Overview
This project demonstrates how to securely enable outbound internet connectivity for resources deployed in a private subnet within an Azure Virtual Network.

In many real-world cloud environments, virtual machines are deployed without public IP addresses to enhance security. However, these machines still require internet access for updates, package installations, and external communication. This project shows how to achieve that using Azure networking components.

---

## 🎯 Objective
- Design a Virtual Network with segmented subnets (public and private)
- Enable controlled outbound internet access from a private subnet
- Implement routing using a Route Table (User Defined Route)
- Deploy and test a Virtual Machine without exposing it publicly
- Use Azure Bastion for secure access

---

## 🏗️ Architecture Summary
The solution follows a secure networking design:

- **Virtual Network (VNet)** acts as the core network
- Two subnets are created:
  - Public Subnet (for external-facing components if needed)
  - Private Subnet (for secure workloads)
- A **Route Table** is configured to control traffic flow
- A **Virtual Machine** is deployed inside the private subnet (no public IP)
- **Azure Bastion** is used for secure, browser-based access
- Outbound internet access is verified using routing (NAT behavior)

---

## 🔐 Key Concepts Used
- Azure Virtual Network (VNet)
- Subnet segmentation (Public vs Private)
- User Defined Routes (UDR)
- NAT-based outbound connectivity
- Azure Bastion (secure access without public IP)
- Secure cloud architecture principles

---

## 🚀 Outcome
By completing this project:
- Private resources can securely access the internet
- No direct public exposure of virtual machines
- Traffic flow is controlled and monitored
- A production-like secure networking setup is achieved

---

## 📂 Use Case
This architecture is commonly used in:
- Enterprise cloud environments
- Secure backend systems
- Applications requiring controlled outbound access
- Zero public exposure infrastructure designs
