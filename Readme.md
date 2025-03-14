# 🚀 Auxiliary API

This project deploys the auxiliary API for retrieving values from AWS services.

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed and configured:

### 1. **Python Version 3** 🛠️  
Install Python from the [official website](https://www.python.org/downloads/).

---

## 🛠️ Setup Instructions and Run

### 1. Install pip
Ensure you have `pip` installed:
```bash
python -m ensurepip --default-pip
```

### 2. Install Dependencies
Install the required Python dependencies:
```bash
pip install Flask==2.3.2 boto3==1.28.32 python-dotenv==1.0.0
```

### 🔑 3. Create a .env File  
Create a `.env` file with the following structure and values:
```bash
AWS_ACCESS_KEY_ID="<<your_access_key>>"
AWS_SECRET_ACCESS_KEY="<<your_secret_access_key>>"
AWS_REGION="<your_region>"
AUXILIARY_SERVICE_VERSION="<your_version>"
PORT="<your_port>"
```

### 4. Run the API
Execute the following command to start the API:
```bash
python auxiliary_service.py
```

## 📡 API Testing Guide

To test API deployments, use the following examples:

### 1. Check API running:
```bash
curl -X GET http://localhost:6000/
```

Expected response:
```Headers
curl: (6) Could not resolve host: GET
HTTP/1.1 404 NOT FOUND
Server: Werkzeug/3.1.3 Python/3.12.4
Date: Thu, 13 Mar 2025 21:30:17 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 207
Connection: close
```
---

## 🚀 GitHub Actions Workflow Definition

This project uses a **CI/CD pipeline** with GitHub Actions to automate Docker image building, pushing to Docker Hub, and updating the Kubernetes deployment with ArgoCD.

### **Workflow Overview**
The workflow consists of two main jobs:
1. **`build-and-push`** – Builds a Docker image for the API and pushes it to Docker Hub.
2. **`deploywithargocd`** – Updates the ArgoCD deployment by modifying the Kubernetes ConfigMap version in the `kantox-k8s` repository.

### **Workflow Steps**
#### 1. **Build and Push Docker Image**
- Runs on a push to the `main` branch.
- Logs into Docker Hub using GitHub Secrets.
- Builds and pushes the API image.

#### 2. **Update Kubernetes ConfigMap and Deploy with ArgoCD**
- Clones the `kantox-k8s` repository.
- Retrieves the current `AUXILIARY_SERVICE_VERSION` from `configmap.yaml`.
- Increments the version number (patch update).
- Commits and pushes the updated `configmap.yaml`.
- ArgoCD will detect the change and automatically deploy the new version.

---
## 🙏 Acknowledgments

- [Python Documentation](https://docs.python.org/3/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [Boto3 Documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)
- [dotenv Documentation](https://pypi.org/project/python-dotenv/)

Happy hacking! 🎉