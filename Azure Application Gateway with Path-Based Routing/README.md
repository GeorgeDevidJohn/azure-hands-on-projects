# Azure Application Gateway with Path-Based Routing

## 1. Project Description

This project demonstrates the deployment and configuration of an Azure Application Gateway (Layer 7 Load Balancer) with path-based routing using the Azure Portal. Incoming HTTP traffic is routed to different backend virtual machines based on URL paths.

The solution includes a secure virtual network design, dedicated subnets, backend virtual machines running Apache web servers, and network security groups for controlled access.

---

## 2. Objectives

- Deploy an Azure Application Gateway with path-based routing  
- Configure a Virtual Network with dedicated subnets  
- Deploy backend Ubuntu virtual machines  
- Install and configure Apache web servers  
- Apply Network Security Groups for security  
- Validate routing and backend health  

---

## 3. Architecture Overview

**Traffic Flow**

Client → Application Gateway (Public IP) → Backend Virtual Machine (based on URL path)

**Backend Routing Rules**
- `/product` → Product Virtual Machine  
- `/cart` → Cart Virtual Machine  

---

## 4. Network Design

### 4.1 Virtual Network

- **VNet Name:** agw-vnet  
- **Address Space:** 10.0.0.0/16  

### 4.2 Subnets

| Subnet Name | Address Range | Purpose |
|------------|---------------|---------|
| agw-subnet | 10.0.0.0/24 | Application Gateway |
| product-subnet | 10.0.1.0/24 | Product VM |
| cart-subnet | 10.0.2.0/24 | Cart VM |

> **Note:** Azure Application Gateway must be deployed in a dedicated subnet.

---

## 5. Network Security Groups

### 5.1 Application Gateway Subnet NSG Rules

| Priority | Rule Name | Port | Source | Action |
|--------|-----------|------|--------|--------|
| 100 | Allow-HTTP | 80 | Internet | Allow |

### 5.2 Virtual Machine Subnet NSG Rules

| Priority | Rule Name | Port | Source | Action |
|--------|-----------|------|--------|--------|
| 100 | Allow-HTTP-from-AGW | 80 | AGW Subnet | Allow |
| 110 | Allow-SSH | 22 | Admin IP | Allow |
| 4096 | Deny-All | * | * | Deny |

---

## 6. Virtual Machine Configuration

### 6.1 VM Specifications

- **Operating System:** Ubuntu 20.04 LTS  
- **VM Size:** Standard B1s  
- **Public IP:** Optional (Not recommended for production)  
- **Authentication:** SSH key or Password  

### 6.2 Apache Web Server Installation

#### Product Virtual Machine

```bash
sudo apt update -y
sudo apt install apache2 -y
sudo mkdir /var/www/html/product
echo "<h1>Product Page</h1>" | sudo tee /var/www/html/product/index.html
