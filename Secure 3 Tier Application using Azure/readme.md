# Secure 3-Tier Python Application on Azure

## Introduction
This project demonstrates the design, deployment, and validation of a **secure 3-tier web application architecture on Microsoft Azure** using Python. It is built to reflect **real-world enterprise standards**, focusing on **network isolation, secure service communication, and cloud-native best practices**.

The solution uses **Azure App Services** for application hosting, **Azure SQL Database** for persistent storage, and **Azure Private Endpoint + VNet Integration** to ensure that sensitive data services are never exposed to the public internet.

This project is suitable for:
- Azure architecture demonstrations
- Proof of Concepts (POC)
- Hands-on learning and training
- Interviews and technical discussions
- Secure cloud application reference implementations

---

## Architecture Overview

### Logical Architecture
The application follows a classic **3-tier architecture**:

1. **Presentation Layer (UI Tier)**  
   - Flask-based web application  
   - Hosted on Azure App Service (Linux)  
   - Publicly accessible over HTTPS  

2. **Application Layer (API Tier)**  
   - FastAPI-based backend service  
   - Hosted on Azure App Service (Linux)  
   - Integrated with Azure Virtual Network  

3. **Data Layer (Database Tier)**  
   - Azure SQL Database  
   - Accessible only via Private Endpoint  
   - Public network access disabled  

### Request Flow
1. User accesses the UI application via browser  
2. UI submits form data to backend API over HTTPS  
3. Backend API connects to Azure SQL Database using private IP  
4. Data is securely stored in the database  
5. Response is returned back to the UI  

At no point is the database exposed to the public internet.

---

## Technology Stack

### Application Stack
- **Language:** Python 3.10 / 3.11
- **Backend Framework:** FastAPI
- **Frontend Framework:** Flask
- **Application Servers:**  
  - Gunicorn (Frontend)  
  - Uvicorn (Backend)
- **Database Driver:** PyODBC

### Azure Services
- Azure App Service (Linux)
- Azure App Service Plan (B1)
- Azure SQL Server
- Azure SQL Database
- Azure Virtual Network (VNet)
- Azure Private Endpoint
- Azure Private DNS Zone

---

## Project Structure

