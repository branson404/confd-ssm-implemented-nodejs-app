# Todo app with Configuration mangement enabled by confd

## 📌 Overview

This project is a simple **Node.js Todo application** enhanced with dynamic configuration management using **confd**.

The application is deployed as a **Kubernetes Pod** and securely retrieves configuration values from **AWS Systems Manager (SSM) Parameter Store** at container startup. This ensures sensitive configuration data (such as secrets and environment variables) are **not hardcoded**, improving security and maintainability.

This project is a simple Nodejs todo-app but we implemneted confd into the app using supervisord and other yaml files that used to deploy it as a kubernetes pod and used service account to connect with AWS SSM and fetch the parameters and values from parameter store in AWS on realtime when container init it sexecuted, this make sure sure security maintains is high and threats from being entered into pods

The system uses:

- **confd** for dynamic configuration management
- **supervisord** for process management inside the container
- **Kubernetes YAML manifests** for deployment
- **Service Account + IAM Role (IRSA)** to securely connect to AWS SSM
- **AWS Parameter Store** for storing runtime configuration

---

## 🏗️ Architecture Overview

1. When the container initializes:
   - `confd` connects to **AWS SSM Parameter Store**
   - It fetches required configuration parameters
   - Generates configuration files or environment variables dynamically

2. `supervisord` ensures:
   - `confd` runs correctly
   - The Node.js app starts after configuration is injected

3. Kubernetes:
   - Deploys the Pod
   - Uses a Service Account mapped to an IAM Role
   - Grants secure access to AWS SSM

---

## Main path why we used confd

- No secrets stored inside the container image
- No sensitive values in Kubernetes manifests
- Secure IAM-based access to AWS SSM
- Runtime configuration injection
- Reduced attack surface inside pods


---
## ⚙️ Technologies Used

- Node.js
- confd
- supervisord
- Kubernetes
- AWS SSM Parameter Store
- IAM Roles for Service Accounts (IRSA)
- Docker

--
## How It Works

### Step 1: Store Parameters in AWS SSM

Used parameters:


"/dev/mongo",
"/dev/port"


---

### Step 2: Deploy to Kubernetes

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```
---
##Build and Run Locally

#Build Docker image:
```bash
docker build -t todo-app .
```
#Run container:
```bash
docker run -p 3000:3000 todo-app
```
