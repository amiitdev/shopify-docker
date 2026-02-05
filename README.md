# 🛍 Shopify Docker – Production-Style Fullstack Setup

A full-stack e-commerce application containerized using Docker with a production-ready architecture and automated CI/CD pipeline.

This project demonstrates real-world DevOps practices including multi-stage Docker builds, Nginx reverse proxy, internal container networking, health monitoring, secure environment configuration, SSH-based Git workflow, GitHub Actions CI/CD automation, and automatic Docker image publishing to Docker Hub.

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
- MongoDB

### DevOps / Infrastructure
- Docker
- Docker Compose
- Nginx Reverse Proxy
- Healthchecks
- GitHub Actions
- Docker Hub

---

## 🏗 Architecture Overview

```
Browser
   ↓
Nginx (Port 80 / 443)
   ↓
/api Reverse Proxy
   ↓
Backend (Internal Docker Network)
```

### CI/CD Flow

```
Developer Pushes Code
        ↓
GitHub Actions Triggered
        ↓
Backend Image Built
Frontend Image Built
        ↓
Images Pushed to Docker Hub
        ↓
Ready for Deployment
```

---

## 🔐 Key Design Decisions

- Backend port is **NOT exposed publicly**
- All traffic flows through Nginx
- `/api` requests are reverse proxied internally
- Containers communicate using Docker internal DNS
- Build stage and runtime stage are separated
- Environment variables injected at runtime
- No secrets stored inside Docker images

---

## 🐳 Run Locally (Development Mode)

Build and start using docker-compose:

```bash
docker compose build
docker compose up
```

Open in browser:

```
http://localhost
```

---

## 🧪 Run Using Docker Hub Images (Production Style)

Pull images built by CI/CD:

```bash
docker pull amiitdev/shopify-backend:latest
docker pull amiitdev/shopify-frontend:latest
```

Run backend with environment variables:

```bash
docker run -p 3000:3000 --env-file server/.env amiitdev/shopify-backend:latest
```

Run frontend:

```bash
docker run -p 80:80 amiitdev/shopify-frontend:latest
```

---

## 🔄 CI/CD Pipeline

Workflow location:

```
.github/workflows/docker-cicd.yml
```

Trigger condition:

```yaml
on:
  push:
    branches:
      - master
```

Every push to `master` automatically:

1. Creates fresh Ubuntu runner  
2. Checks out repository  
3. Logs into Docker Hub securely  
4. Builds backend Docker image  
5. Builds frontend Docker image  
6. Pushes both images to Docker Hub  

No manual `docker build` or `docker push` required.

---

## 🩺 Healthcheck

Backend includes:

```http
GET /health
```

Docker monitors container health automatically.

---

## 📦 Project Structure

```
client/
  ├── Dockerfile
  ├── nginx.conf
  └── src/

server/
  ├── Dockerfile
  ├── api/
  └── .dockerignore

.github/workflows/docker-cicd.yml
docker-compose.yml
README.md
```

---

## 🎯 What This Project Demonstrates

- Docker multi-stage builds  
- Reverse proxy architecture  
- Secure container networking  
- Separation of configuration from code  
- CI/CD automation with GitHub Actions  
- Docker Hub registry integration  
- Production-ready container workflow  

---

## 👨‍💻 Author

Amit Kumar  
DevOps / Fullstack Developer
