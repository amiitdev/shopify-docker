# 🛍 Shopify – Fullstack DevOps Deployment (Docker + Kubernetes)

A production-style full-stack e-commerce application deployed using Docker and Kubernetes with CI/CD automation.

This project demonstrates real-world DevOps practices including containerization, reverse proxy architecture, Kubernetes orchestration, internal service discovery, health monitoring, rolling updates, resource management, secret injection, and automated Docker image publishing via GitHub Actions.

---

# 🚀 Tech Stack

## Frontend
- React (Vite)
- Axios
- Nginx (Production Serving & Reverse Proxy)

## Backend
- Node.js
- Express.js
- REST API
- MongoDB Atlas

## DevOps / Infrastructure
- Docker & Docker Compose
- Kubernetes (Minikube)
- Kubernetes Deployments & Services
- Ingress Controller (NGINX)
- Liveness & Readiness Probes
- Resource Requests & Limits
- Kubernetes Secrets
- GitHub Actions (CI/CD)
- Docker Hub

---

# 🏗 Architecture Overview

## 1️⃣ Docker Architecture (Container Level)

```
Browser
   ↓
Nginx (Port 80)
   ↓
/api Reverse Proxy
   ↓
Backend Container (Internal Docker Network)
   ↓
MongoDB Atlas
```

- Backend port is NOT exposed publicly
- All API traffic flows through Nginx
- Containers communicate via Docker internal DNS

---

## 2️⃣ Kubernetes Architecture (Cluster Level)

```
Browser
   ↓
Ingress (shopify.local)
   ↓
Frontend Service (ClusterIP)
   ↓
Frontend Pod
   ↓
Backend Service (ClusterIP)
   ↓
Backend Pods (2 Replicas)
   ↓
MongoDB Atlas
```

### Key Concepts Used:
- ClusterIP for internal service discovery
- Ingress for external routing
- Multi-replica backend for high availability
- Health probes for self-healing
- Rolling updates for zero downtime

---

# 🐳 Docker Usage

## Build & Run (Development)

```bash
docker compose build
docker compose up
```

Access:
```
http://localhost
```

## Run Using Docker Hub Images (Production Style)

```bash
docker pull amiitdev/shopify-backend:latest
docker pull amiitdev/shopify-frontend:latest
```

Run backend:

```bash
docker run -p 3000:3000 --env-file server/.env amiitdev/shopify-backend:latest
```

Run frontend:

```bash
docker run -p 80:80 amiitdev/shopify-frontend:latest
```

---

# ☸ Kubernetes Deployment (Minikube)

## Step 1 — Start Cluster

```bash
minikube start --driver=docker
```

## Step 2 — Enable Ingress Controller

```bash
minikube addons enable ingress
```

Verify:

```bash
kubectl get pods -n ingress-nginx
```

---

## Step 3 — Create Kubernetes Secret

Secrets are NOT stored in Git.

Create from env file:

```bash
kubectl create secret generic shopify-secret \
  --from-env-file=server/.env
```

Verify:

```bash
kubectl get secrets
```

---

## Step 4 — Apply Manifests

```bash
kubectl apply -f k8s/
```

Check resources:

```bash
kubectl get pods
kubectl get svc
kubectl get ingress
```

---

## Step 5 — Configure Local Domain

Get Minikube IP:

```bash
minikube ip
```

Edit `/etc/hosts`:

```
<minikube-ip> shopify.local
```

Access:

```
http://shopify.local
```

---

# 🩺 Health Monitoring

Backend exposes:

```
GET /health
```

### Readiness Probe
- Controls when pod receives traffic
- Prevents sending traffic to unready pods

### Liveness Probe
- Automatically restarts unhealthy containers
- Enables self-healing behavior

---

# 📈 Scaling & Rolling Updates

Scale backend manually:

```bash
kubectl scale deployment backend-deployment --replicas=3
```

Restart deployment:

```bash
kubectl rollout restart deployment backend-deployment
```

Check rollout status:

```bash
kubectl rollout status deployment/backend-deployment
```

---

# 🔐 Security & Configuration

- No secrets committed to Git
- Kubernetes Secret used for sensitive environment variables
- Backend exposed internally only (ClusterIP)
- Frontend exposed via Ingress
- Resource limits prevent resource exhaustion

Example resource configuration:

```yaml
resources:
  requests:
    memory: "128Mi"
    cpu: "100m"
  limits:
    memory: "256Mi"
    cpu: "500m"
```

---

# 🔄 CI/CD Pipeline

Workflow location:

```
.github/workflows/docker-cicd.yml
```

On every push to `master`:

1. GitHub Actions runner starts
2. Backend Docker image built
3. Frontend Docker image built
4. Images pushed to Docker Hub
5. Ready for Kubernetes deployment

Images:

```
amiitdev/shopify-backend:latest
amiitdev/shopify-frontend:latest
```

---

# 📂 Project Structure

```
client/
server/
k8s/
.github/workflows/
docker-compose.yml
README.md
```

---

# 🎯 What This Project Demonstrates

- Docker multi-stage builds
- Reverse proxy architecture
- Kubernetes Deployments & Services
- Internal DNS-based service discovery
- Ingress routing with custom domain
- Health probes & self-healing pods
- Resource management
- Rolling updates without downtime
- Secure secret management
- CI/CD automation with GitHub Actions
- Docker Hub registry integration

---

# 👨‍💻 Author

Amit Kumar  
DevOps / Fullstack Engineer
