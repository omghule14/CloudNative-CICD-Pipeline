# 🚀 CI/CD Pipeline for 3-Tier Application Deployment

A complete **DevOps CI/CD project** demonstrating automated build, containerization, testing, and deployment of a **3-tier web application** using **GitHub Actions, Docker, Kubernetes, Nginx, and MySQL**.

The project implements a practical software delivery workflow where source-code changes trigger automated CI/CD processes and containerized applications are deployed using Kubernetes.

---

## 📌 Project Overview

This project demonstrates how a traditional 3-tier application can be containerized and deployed using modern DevOps practices.

The application consists of three primary layers:

```text
┌───────────────────────────────┐
│           Frontend            │
│        HTML / CSS / JS        │
│            Nginx              │
└───────────────┬───────────────┘
                │
                │ HTTP / API
                ▼
┌───────────────────────────────┐
│           Backend             │
│            Go API             │
│            :8080              │
└───────────────┬───────────────┘
                │
                │ SQL
                ▼
┌───────────────────────────────┐
│            MySQL              │
│          Database             │
│            :3306              │
└───────────────────────────────┘
```

The complete DevOps workflow is:

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ├── Build
    ├── Test
    ├── Docker Build
    └── Docker Push
             │
             ▼
        Docker Hub
             │
             ▼
        Kubernetes
             │
             ▼
      3-Tier Application
```

---

# 🎯 Project Objectives

* Build a complete CI/CD pipeline using GitHub Actions
* Containerize frontend and backend applications using Docker
* Run the complete application locally using Docker Compose
* Use Nginx as a reverse proxy
* Deploy the application using Kubernetes
* Use MySQL as the persistent database
* Automate Docker image creation and publishing
* Implement Kubernetes rolling deployments
* Manage configuration using environment variables and Kubernetes resources
* Practice real-world DevOps deployment workflows

---

# 🧰 Technology Stack

| Category                | Technology                                 |
| ----------------------- | ------------------------------------------ |
| Source Control          | Git, GitHub                                |
| CI/CD                   | GitHub Actions                             |
| Frontend                | HTML, CSS, JavaScript                      |
| Web Server              | Nginx                                      |
| Backend                 | Go / Gin                                   |
| Database                | MySQL 8.4                                  |
| Containerization        | Docker                                     |
| Local Orchestration     | Docker Compose                             |
| Container Registry      | Docker Hub                                 |
| Container Orchestration | Kubernetes                                 |
| Local Kubernetes        | Kind                                       |
| Configuration           | Environment Variables, ConfigMaps, Secrets |

---

# 🏗️ System Architecture

```text
                         ┌─────────────────┐
                         │    Developer    │
                         └────────┬────────┘
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
                       │      CI/CD          │
                       └──────────┬──────────┘
                                  │
                    ┌─────────────┴─────────────┐
                    │                           │
                    ▼                           ▼
             Build & Test                Docker Build
                                                │
                                                ▼
                                          Docker Hub
                                                │
                                                ▼
                                         Kubernetes
                                                │
                  ┌─────────────────────────────┼─────────────────────────┐
                  │                             │                         │
                  ▼                             ▼                         ▼
           ┌─────────────┐              ┌─────────────┐           ┌─────────────┐
           │  Frontend   │              │   Backend   │           │    MySQL    │
           │    Nginx    │─────────────▶│    Go API   │──────────▶│  Database   │
           │     :80     │              │    :8080    │           │    :3306    │
           └─────────────┘              └─────────────┘           └─────────────┘
```

---

# 📂 Project Structure

```text
CI-CD-Pipeline-3-Tier-Application/
│
├── .github/
│   └── workflows/
│       ├── ci.yml
│       ├── cd.yml
│       └── cd-k8s.yml
│
├── backend/
│   ├── Dockerfile
│   ├── main.go
│   └── ...
│
├── frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   ├── index.html
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

# 🐳 Docker Compose Deployment

Docker Compose is used to run the complete 3-tier application locally.

## Prerequisites

Install:

* Git
* Docker Desktop
* Docker Compose

Verify the installation:

```bash
docker --version
docker compose version
```

---

## 1. Clone the Repository

```bash
git clone https://github.com/omghule14/REPOSITORY-NAME.git
```

```bash
cd REPOSITORY-NAME
```

Replace `REPOSITORY-NAME` with your actual GitHub repository name.

---

## 2. Create Environment File

### Windows CMD

```cmd
copy .env.example .env
```

### Linux / macOS

```bash
cp .env.example .env
```

Configure the required environment variables in `.env`.

> ⚠️ Never commit `.env` or passwords to GitHub.

---

## 3. Build and Start Containers

```bash
docker compose up -d --build
```

This starts:

```text
Frontend
Backend
MySQL
```

---

## 4. Check Running Containers

```bash
docker compose ps
```

or:

```bash
docker ps
```

---

## 5. Access the Application

Open:

```text
http://localhost
```

The frontend is served through Nginx.

---

# 🔀 Nginx Reverse Proxy

Nginx acts as the entry point for the application.

```text
                     Client
                       │
                       │ HTTP :80
                       ▼
                ┌──────────────┐
                │    Nginx     │
                │   Frontend   │
                └──────┬───────┘
                       │
                       │ /api/
                       ▼
                ┌──────────────┐
                │   Backend    │
                │   Go / Gin   │
                │    :8080     │
                └──────┬───────┘
                       │
                       │ MySQL
                       ▼
                ┌──────────────┐
                │    MySQL     │
                │    :3306     │
                └──────────────┘
```

This allows the frontend and backend to be accessed through a single application endpoint.

---

# 🔄 CI/CD Pipeline

GitHub Actions automates the application's build and deployment lifecycle.

```text
Developer
    │
    │ git push
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Checkout Code
    │
    ├── Build Application
    │
    ├── Run Tests
    │
    ├── Build Docker Images
    │
    ├── Tag Images
    │
    └── Push Images
           │
           ▼
       Docker Hub
           │
           ▼
      Kubernetes
           │
           ▼
     Application
```

---

# ⚙️ GitHub Actions

The CI/CD workflows are stored inside:

```text
.github/workflows/
```

The pipeline can automate:

### Continuous Integration

1. Checkout source code
2. Install dependencies
3. Run tests
4. Build the application
5. Build Docker images

### Continuous Delivery

1. Authenticate with Docker Hub
2. Push Docker images
3. Update Kubernetes deployment
4. Deploy the latest version
5. Verify deployment status

---

# 🐳 Docker Images

The project contains separate Docker images for the application components.

Example:

```text
Frontend Image
        │
        ▼
Nginx Container

Backend Image
        │
        ▼
Go API Container

MySQL Image
        │
        ▼
Database Container
```

Docker images can be published to Docker Hub and later pulled by Kubernetes.

---

# ☸️ Kubernetes Deployment

The application can also be deployed to Kubernetes using **Kind** for local development.

## Prerequisites

Install:

```bash
Docker Desktop
kubectl
Kind
```

Verify:

```bash
docker --version
kubectl version --client
kind version
```

---

## Create Kubernetes Cluster

If the project Makefile provides the required configuration:

```bash
make up
```

---

## Check Kubernetes Nodes

```bash
kubectl get nodes
```

---

## Check Pods

```bash
kubectl get pods
```

---

## Check Services

```bash
kubectl get services
```

---

## Check Deployments

```bash
kubectl get deployments
```

---

# ☸️ Kubernetes Architecture

```text
                    Kubernetes Cluster
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐
   │  Frontend   │  │   Backend   │  │    MySQL    │
   │ Deployment  │  │ Deployment  │  │ StatefulSet │
   └──────┬──────┘  └──────┬──────┘  └──────┬──────┘
          │                │                │
          ▼                ▼                ▼
   Frontend Service  Backend Service   MySQL Service
          │                │                │
          └────────────────┴────────────────┘
```

---

# 🔐 Configuration & Secrets

Sensitive information should never be hard-coded into the application or committed to GitHub.

The project can use:

* `.env`
* Kubernetes Secrets
* Kubernetes ConfigMaps
* GitHub Actions Secrets

Typical sensitive values include:

```text
DB_PASSWORD
DOCKERHUB_USERNAME
DOCKERHUB_TOKEN
```

GitHub Actions secrets can be configured from:

```text
GitHub Repository
      ↓
Settings
      ↓
Secrets and variables
      ↓
Actions
```

---

# 🗄️ MySQL Database

MySQL is used as the database layer of the application.

Database initialization is handled through:

```text
mysql/init.sql
```

With Docker Compose:

```text
Backend Container
       │
       │ db:3306
       ▼
MySQL Container
```

With Kubernetes:

```text
Backend Pod
     │
     │ MySQL Service
     ▼
MySQL Pod
```

---

# 🩺 Health Checks

Health checks help verify that application services are available.

Example backend endpoint:

```text
GET /health
```

Health checks can be used by Docker and Kubernetes to determine whether the application is ready to receive traffic.

---

# 🛠️ Useful Docker Commands

### Start

```bash
docker compose up -d
```

### Build and Start

```bash
docker compose up -d --build
```

### Stop

```bash
docker compose down
```

### Check Containers

```bash
docker compose ps
```

### View All Logs

```bash
docker compose logs
```

### Backend Logs

```bash
docker compose logs backend
```

### Frontend Logs

```bash
docker compose logs frontend
```

### Database Logs

```bash
docker compose logs db
```

---

# 🛠️ Useful Kubernetes Commands

### View Pods

```bash
kubectl get pods
```

### View Services

```bash
kubectl get svc
```

### View Deployments

```bash
kubectl get deployments
```

### View Pod Logs

```bash
kubectl logs <pod-name>
```

### Describe Pod

```bash
kubectl describe pod <pod-name>
```

### Check Deployment Rollout

```bash
kubectl rollout status deployment/<deployment-name>
```

### Restart Deployment

```bash
kubectl rollout restart deployment/<deployment-name>
```

---

# 🧪 Troubleshooting

### Docker Containers Not Starting

```bash
docker compose ps
```

Check logs:

```bash
docker compose logs
```

### Check Docker Images

```bash
docker images
```

### Check Kubernetes Pods

```bash
kubectl get pods
```

### Check Kubernetes Events

```bash
kubectl get events --sort-by=.lastTimestamp
```

### Check Services

```bash
kubectl get svc
```

---

# 📈 DevOps Concepts Demonstrated

This project provides hands-on experience with:

### Git & GitHub

* Git repository management
* Branching
* Commits
* Remote repositories
* Pull requests

### Docker

* Dockerfiles
* Docker images
* Container networking
* Docker Compose
* Multi-container applications

### GitHub Actions

* CI/CD workflows
* Automated builds
* Automated testing
* Docker image publishing
* Deployment automation

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

* Continuous Integration
* Continuous Delivery
* Containerization
* Infrastructure automation
* Application deployment
* Service discovery
* Troubleshooting

---

# 🔮 Future Enhancements

Planned improvements include:

* ☁️ Deploy the application to AWS EKS
* ⚖️ Configure AWS Application Load Balancer
* 🌐 Implement Kubernetes Ingress
* 📈 Add Horizontal Pod Autoscaling
* 📦 Introduce Helm charts
* 🔄 Implement GitOps using Argo CD
* 📊 Add Prometheus and Grafana monitoring
* 📝 Implement centralized logging
* 🔐 Integrate AWS Secrets Manager
* 🛡️ Add container vulnerability scanning
* 🚀 Implement blue-green or canary deployments

---

# 📚 Learning Outcomes

By completing this project, I gained practical experience in:

* Designing a 3-tier application architecture
* Containerizing applications using Docker
* Managing multi-container applications with Docker Compose
* Creating CI/CD pipelines using GitHub Actions
* Building and publishing Docker images
* Deploying applications to Kubernetes
* Managing Kubernetes Deployments and Services
* Working with persistent database storage
* Managing application configuration and secrets
* Implementing health checks
* Troubleshooting containerized applications
* Understanding the complete CI/CD lifecycle

---

# 👨‍💻 Author

## Om Ghule

GitHub:
https://github.com/omghule14

---

## ⭐ Project

**CI/CD Pipeline for 3-Tier Application Deployment**

A hands-on DevOps project demonstrating automated application delivery using **GitHub Actions, Docker, Docker Hub, Kubernetes, Nginx, Go, and MySQL**.
