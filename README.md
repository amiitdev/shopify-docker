# 🛍 Shopify – Production-Style Fullstack (Docker + Kubernetes)

A full-stack e-commerce application built with **React, Node.js, Docker, and Kubernetes**, following real-world DevOps and production architecture practices.

This project demonstrates containerization, reverse proxy setup, Kubernetes deployments, service discovery, health monitoring, rolling updates, secret management, and CI/CD automation with Docker Hub integration.

---

## 🚀 Tech Stack

### Frontend
- React (Vite)
- Axios
- Nginx (Production Serving)

### Backend
- Node.js
- Express.js
- REST API
- MongoDB Atlas

### DevOps / Infrastructure
- Docker & Docker Compose
- Kubernetes (Minikube)
- Nginx Reverse Proxy
- Kubernetes Ingress
- Liveness & Readiness Probes
- Kubernetes Secrets
- GitHub Actions (CI/CD)
- Docker Hub

---

## 🏗 Architecture Overview

### Docker Architecture

```
Browser
   ↓
Nginx (Port 80)
   ↓
/api Reverse Proxy
   ↓
Backend (Internal Docker Network)
   ↓
MongoDB Atlas
```

### Kubernetes Architecture

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

---

## ☸ Kubernetes Setup

- Backend Deployment (2 replicas)
- Frontend Deployment
- ClusterIP Services
- Ingress routing (`shopify.local`)
- Health Probes for self-healing
- Resource requests & limits
- Secrets injected securely (not committed to Git)

---

## 🔄 CI/CD Pipeline

Workflow location:

```
.github/workflows/docker-cicd.yml
```

On every push to `master`:
- Builds backend Docker image
- Builds frontend Docker image
- Pushes images to Docker Hub
- Ready for Kubernetes deployment

Docker Images:
```
amiitdev/shopify-backend:latest
amiitdev/shopify-frontend:latest
```

---

## 🧪 Run Locally (Docker)

```bash
docker compose build
docker compose up
```

Open:
```
http://localhost
```

---

## ☸ Deploy on Kubernetes (Minikube)

```bash
minikube start --driver=docker
minikube addons enable ingress
kubectl apply -f k8s/
```

Add to `/etc/hosts`:

```
<minikube-ip> shopify.local
```

Access:
```
http://shopify.local
```

---

## 🩺 Health Monitoring

Backend exposes:
```
GET /health
```

Kubernetes:
- Uses Readiness Probe to control traffic
- Uses Liveness Probe to auto-restart unhealthy pods
- Enables zero-downtime rolling updates

---

## 📦 Project Structure

```
client/
server/
k8s/
.github/workflows/
docker-compose.yml
README.md
```

---

## 🎯 What This Project Demonstrates

- Docker multi-stage builds  
- Reverse proxy architecture  
- Kubernetes deployments & services  
- Ingress-based routing  
- Service discovery via ClusterIP  
- Health checks & self-healing  
- Secure secret management  
- Rolling updates without downtime  
- CI/CD automation with GitHub Actions  

---

**Author:** Amit Kumar  
DevOps / Fullstack Engineer
