# 🚀 CloudNative-CICD-Pipeline

## Automated CI/CD Pipeline with Docker & Kubernetes

A production-style cloud-native application demonstrating **CI/CD automation, Docker containerization, Kubernetes orchestration, and MySQL database integration**.

This project implements an end-to-end DevOps workflow using **GitHub Actions, Docker, Docker Hub, Kubernetes, Nginx, Go, and MySQL**. The goal is to automate application build, containerization, image publishing, and Kubernetes deployment.

---

## 📌 Project Overview

**CloudNative-CICD-Pipeline** is a three-tier application designed to demonstrate a practical DevOps and cloud-native deployment workflow.

The project covers the complete application delivery lifecycle:

```text
Developer
    ↓
GitHub
    ↓
GitHub Actions
    ↓
Build & Test
    ↓
Docker Images
    ↓
Docker Hub
    ↓
Kubernetes
    ↓
Application Deployment
```

### Key Objectives

* Containerize frontend and backend applications
* Run multiple services using Docker Compose
* Automate CI/CD using GitHub Actions
* Build and publish Docker images
* Deploy applications to Kubernetes
* Manage application configuration and secrets
* Run MySQL as the persistent database layer
* Implement health checks and rolling deployments
* Practice real-world DevOps workflows

---

## 🏗️ Architecture

```text
                         Developer
                             │
                             │ git push
                             ▼
                    ┌─────────────────┐
                    │     GitHub      │
                    │   Repository    │
                    └────────┬────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │   GitHub Actions    │
                  │       CI/CD         │
                  └──────────┬──────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │     Docker      │
                    │ Build & Test    │
                    └────────┬────────┘
                             │
                             ▼
                       Docker Hub
                             │
                             ▼
                     ┌───────────────┐
                     │  Kubernetes   │
                     │    Cluster    │
                     └───────┬───────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
              ▼              ▼              ▼
         Frontend         Backend         MySQL
          Nginx            Go API        Database
```

---

## 🧰 Technology Stack

| Category           | Technology                                  |
| ------------------ | ------------------------------------------- |
| Frontend           | HTML, CSS, JavaScript                       |
| Web Server         | Nginx                                       |
| Backend            | Go / Gin                                    |
| Database           | MySQL 8.4                                   |
| Containerization   | Docker                                      |
| Orchestration      | Kubernetes                                  |
| Local Kubernetes   | Kind                                        |
| CI/CD              | GitHub Actions                              |
| Container Registry | Docker Hub                                  |
| Source Control     | Git & GitHub                                |
| Configuration      | Environment Variables, ConfigMaps & Secrets |

---

## 📁 Project Structure

```text
CloudNative-CICD-Pipeline/
│
├── .github/
│   └── workflows/
│
├── backend/
│   ├── Dockerfile
│   └── ...
│
├── frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── ...
│
├── mysql/
│   └── init.sql
│
├── k8s/
│   ├── kind-config.yaml
│   ├── namespace.yaml
│   ├── mysql.yaml
│   ├── backend.yaml
│   └── frontend.yaml
│
├── docs/
│
├── docker-compose.yml
├── .env.example
├── .gitignore
├── Makefile
└── README.md
```

---

## 🐳 Run Locally with Docker Compose

### Prerequisites

Install:

* Git
* Docker Desktop
* Docker Compose

Verify:

```bash
docker --version
docker compose version
```

### 1. Clone the repository

```bash
git clone https://github.com/omghule14/CloudNative-CICD-Pipeline.git
cd CloudNative-CICD-Pipeline
```

### 2. Create environment configuration

Linux/macOS:

```bash
cp .env.example .env
```

Windows CMD:

```cmd
copy .env.example .env
```

Update `.env` with the required configuration.

### 3. Build and start

```bash
docker compose up -d --build
```

### 4. Check containers

```bash
docker compose ps
```

or:

```bash
docker ps
```

### 5. Access the application

```text
http://localhost
```

---

## 🔄 CI/CD Pipeline

The GitHub Actions pipeline automates the software delivery process.

```text
Git Push
   │
   ▼
GitHub Actions
   │
   ├── Checkout Code
   │
   ├── Build Backend
   │
   ├── Build Frontend
   │
   ├── Run Tests / Validation
   │
   ├── Build Docker Images
   │
   └── Push Images to Docker Hub
                │
                ▼
          Docker Registry
                │
                ▼
           Kubernetes
                │
                ▼
          Application
```

### CI Responsibilities

* Checkout source code
* Validate application
* Build Docker images
* Tag images
* Push images to Docker Hub

### CD Responsibilities

* Retrieve the latest container images
* Update Kubernetes deployments
* Perform rolling updates
* Verify deployment status

---

## ☸️ Kubernetes Deployment

The project supports deployment to a local Kubernetes cluster using **Kind**.

### Prerequisites

```bash
docker --version
kubectl version --client
kind version
```

### Create the cluster

```bash
make up
```

### Check cluster

```bash
kubectl get nodes
```

### Check pods

```bash
kubectl get pods -A
```

### Check services

```bash
kubectl get services -A
```

### Check deployments

```bash
kubectl get deployments -A
```

---

## 🔐 Security & Configuration

Sensitive information should never be committed to GitHub.

The project uses:

* `.env` for local configuration
* Kubernetes Secrets for sensitive Kubernetes configuration
* GitHub Actions Secrets for CI/CD credentials

Sensitive files should remain excluded from Git:

```text
.env
*.pem
private keys
passwords
API tokens
Docker Hub credentials
```

---

## 🗄️ Database

The application uses **MySQL 8.4** as its database layer.

The database is initialized using:

```text
mysql/init.sql
```

With Docker Compose, the database runs as a separate container.

With Kubernetes, MySQL is deployed separately and accessed by the backend through Kubernetes service discovery.

```text
Backend
   │
   │ mysql-service:3306
   ▼
MySQL
```

---

## 🌐 Nginx Reverse Proxy

Nginx acts as the frontend web server and reverse proxy.

```text
Client
  │
  ▼
Nginx :80
  │
  ├── Static Frontend
  │
  └── /api/
        │
        ▼
      Backend :8080
```

This provides a single entry point for users while keeping the backend service isolated from direct external access.

---

## 🩺 Health Checks

Health checks are used to verify application availability.

Example:

```text
GET /health
```

Health checks help Docker and Kubernetes determine whether the application is ready to receive traffic.

---

## 🛠️ Useful Docker Commands

### Start

```bash
docker compose up -d
```

### Rebuild

```bash
docker compose up -d --build
```

### Stop

```bash
docker compose down
```

### View containers

```bash
docker compose ps
```

### View logs

```bash
docker compose logs
```

### View backend logs

```bash
docker compose logs backend
```

### View frontend logs

```bash
docker compose logs frontend
```

### View database logs

```bash
docker compose logs db
```

---

## 🛠️ Useful Kubernetes Commands

### Pods

```bash
kubectl get pods
```

### Services

```bash
kubectl get svc
```

### Deployments

```bash
kubectl get deployments
```

### Pod logs

```bash
kubectl logs <pod-name>
```

### Describe resource

```bash
kubectl describe pod <pod-name>
```

### Deployment status

```bash
kubectl rollout status deployment/<deployment-name>
```

### Restart deployment

```bash
kubectl rollout restart deployment/<deployment-name>
```

---

## 🎯 DevOps Skills Demonstrated

This project demonstrates practical experience with:

### Git & GitHub

* Git repositories
* Branch management
* Commits
* Remote repositories
* GitHub workflows

### Docker

* Dockerfiles
* Docker images
* Container networking
* Docker Compose
* Environment variables

### GitHub Actions

* CI/CD workflows
* Automated builds
* Docker image publishing
* Deployment automation
* Secrets management

### Kubernetes

* Pods
* Deployments
* Services
* StatefulSets
* ConfigMaps
* Secrets
* Persistent storage
* Health probes
* Rolling updates

### DevOps Practices

* Infrastructure automation
* Continuous integration
* Continuous deployment
* Containerization
* Service discovery
* Application monitoring
* Troubleshooting

---

## 🔮 Future Improvements

Planned improvements include:

* Deploy to AWS EKS
* Add AWS Application Load Balancer
* Implement Kubernetes Ingress
* Add Horizontal Pod Autoscaling
* Introduce Helm charts
* Implement GitOps using Argo CD
* Add Prometheus and Grafana
* Add centralized logging
* Integrate AWS Secrets Manager
* Add container vulnerability scanning
* Implement blue-green/canary deployments

---

## 👨‍💻 Author

### Om Ghule

**GitHub:**
[https://github.com/omghule14](https://github.com/omghule14)

---

## ⭐ Project

**CloudNative-CICD-Pipeline**

A hands-on DevOps project demonstrating how a containerized application can be built, tested, packaged, and deployed using modern CI/CD and Kubernetes practices.
