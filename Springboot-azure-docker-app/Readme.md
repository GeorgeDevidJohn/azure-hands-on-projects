# 🚀 Spring Boot Deployment to Azure using Docker & ACR

## 📌 Overview

This project demonstrates how to deploy the Spring PetClinic application
to Microsoft Azure using Docker and Azure cloud services.

The application is:

-   Built using Maven\
-   Containerized using Docker\
-   Pushed to DockerHub & Azure Container Registry (ACR)\
-   Deployed to Azure App Service (Linux)

------------------------------------------------------------------------

## 🛠 Technologies Used

-   Microsoft Azure\
-   Docker\
-   Azure Container Registry (ACR)\
-   Azure App Service\
-   Apache Maven\
-   OpenJDK 17\
-   Git

------------------------------------------------------------------------

## 🔄 Deployment Flow

GitHub → Azure VM → Maven Build → Docker Image\
↓\
DockerHub / Azure ACR\
↓\
Azure App Service (Linux)\
↓\
Live Web Application

------------------------------------------------------------------------

## ▶️ Run Locally

### 1️⃣ Build the application

``` bash
mvn clean package
```

### 2️⃣ Build Docker image

``` bash
docker build -t petclinic .
```

### 3️⃣ Run container

``` bash
docker run -p 8080:8080 petclinic
```

Access in browser:

    http://localhost:8080

------------------------------------------------------------------------

## 📚 Learning Outcomes

-   Azure VM provisioning\
-   Maven build lifecycle\
-   Docker containerization\
-   Image registry management\
-   Cloud deployment using Azure

------------------------------------------------------------------------

## ✅ Status

✔ Successfully deployed to Azure App Service using Docker container.
