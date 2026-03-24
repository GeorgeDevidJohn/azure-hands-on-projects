# 🚀 Hub-and-Spoke Architecture with Azure Firewall

## 📌 Introduction
Cloud network security is a critical aspect of modern cloud infrastructure. In Microsoft Azure, the **Hub-and-Spoke architecture** is widely used to centralize security, connectivity, and traffic control.

This project demonstrates the implementation of a **Hub-and-Spoke Virtual Network architecture** using Azure. The **Hub network** contains an **Azure Firewall** acting as the central security layer, while the **Spoke network** hosts a virtual machine generating traffic.

The firewall is configured with:
- 🔹 NAT Rules  
- 🔹 Network Rules  
- 🔹 Application Rules  

This setup ensures:
- Controlled outbound traffic  
- Access restricted to **Google services only**  
- Blocking of all other internet traffic  

---

## 🏗️ Architecture Overview

### 🔹 Components

#### Hub Network
- Hub Virtual Network (`hub-vnet`)
- Azure Firewall (`hub-firewall`)
- AzureFirewallSubnet

#### Spoke Network
- Spoke Virtual Network (`spoke-vnet`)
- Virtual Machine (`spoke-vm`)
- Workload Subnet (`workload-subnet`)

#### Connectivity
- VNet Peering (Hub ↔ Spoke)
- Route Table (forces traffic through firewall)

### 🔄 Traffic Flow


Spoke VM → Route Table → Azure Firewall (Hub) → Internet (Google Only)


---

## 📋 Prerequisites
Before starting, ensure you have:

- ✅ Active **Microsoft Azure Subscription**
- ✅ Access to **Azure Portal**
- ✅ Basic knowledge of **Virtual Networks**
- ✅ Created **Resource Group**

---

## ⚙️ Deployment Steps

### 🔹 Step 1 – Create Resource Group
- Name: `hub-spoke-rg`
- Region: `Canada Central`

---

### 🔹 Step 2 – Create Hub Virtual Network
- Name: `hub-vnet`
- Address Space: `10.0.0.0/16`

**Subnet**
- Name: `AzureFirewallSubnet`
- Address Range: `10.0.1.0/24`

> ⚠️ Required: Subnet must be named `AzureFirewallSubnet`

---

### 🔹 Step 3 – Create Spoke Virtual Network
- Name: `spoke-vnet`
- Address Space: `10.1.0.0/16`

**Subnet**
- Name: `workload-subnet`
- Address Range: `10.1.1.0/24`

---

### 🔹 Step 4 – Configure VNet Peering

#### Hub → Spoke
- Peering Name: `hub-to-spoke`
- Enable:
  - Allow forwarded traffic
  - Allow gateway transit

#### Spoke → Hub
- Peering Name: `spoke-to-hub`
- Enable:
  - Allow forwarded traffic
  - Use remote gateway

---

### 🔹 Step 5 – Deploy Azure Firewall
- Name: `hub-firewall`
- Region: `Canada Central`
- VNet: `hub-vnet`
- Subnet: `AzureFirewallSubnet`
- Public IP: Create new

⏳ Deployment time: ~5–10 minutes

---

### 🔹 Step 6 – Create Route Table
- Name: `spoke-route-table`

---

### 🔹 Step 7 – Add Route to Firewall
| Setting            | Value                  |
|-------------------|------------------------|
| Route Name        | default-route          |
| Address Prefix    | 0.0.0.0/0              |
| Next Hop Type     | Virtual Appliance      |
| Next Hop Address  | Firewall Private IP    |

---

### 🔹 Step 8 – Associate Route Table
- Virtual Network: `spoke-vnet`
- Subnet: `workload-subnet`

---

### 🔹 Step 9 – Create Virtual Machine
- VM Name: `spoke-vm`
- OS: Ubuntu
- VNet: `spoke-vnet`
- Subnet: `workload-subnet`

📷 *Add Screenshot Here*

---

### 🔹 Step 10 – Configure Application Rule (Allow Google)

| Setting        | Value           |
|----------------|-----------------|
| Name           | allow-google    |
| Priority       | 100             |
| Action         | Allow           |

**Rule:**
- Source: `10.1.1.0/24`
- Protocol: HTTP, HTTPS
- Target FQDN: `*.google.com`

---

### 🔹 Step 11 – Configure NAT Rule (Optional)

| Setting              | Value                 |
|---------------------|----------------------|
| Name                | ssh-nat              |
| Source              | Any                  |
| Destination         | Firewall Public IP   |
| Protocol            | TCP                  |
| Port                | 22                   |
| Translated Address  | VM Private IP        |

---

### 🔹 Step 12 – Test Connectivity

Connect via SSH or Azure Bastion and run:

```bash
# Test allowed traffic
curl https://www.google.com

# Test blocked traffic
curl https://www.facebook.com

✅ Expected Results

Google → ✅ Accessible

Other websites → ❌ Blocked

📊 Key Learnings

Centralized traffic control using Azure Firewall

Secure outbound connectivity using UDR + Firewall

Domain-based filtering using Application Rules

Real-world enterprise network architecture design

Troubleshooting using logs and connectivity testing

🏁 Conclusion

This project successfully demonstrates a secure Hub-and-Spoke architecture in Microsoft Azure.

All traffic from the spoke network is routed through the firewall

Access is restricted using application rules

Only Google services are allowed, ensuring strict policy enforcement

This architecture provides:

🔒 Centralized security

📈 Scalable network design

⚡ Efficient traffic management
