# 🛍 Shopify Docker – Production-Style Fullstack Setup

A full-stack e-commerce application containerized using Docker with a production-ready architecture.

This project demonstrates real-world DevOps practices including:

- Multi-stage Docker builds
- Nginx reverse proxy
- Internal container networking
- Health monitoring
- Secure environment configuration
- SSH-based Git workflow

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

### DevOps / Infrastructure
- Docker
- Docker Compose
- Nginx Reverse Proxy
- Healthchecks
- HTTPS Support

---

## 🏗 Architecture Overview


### 🔐 Key Design Decisions

- Backend port is **NOT exposed publicly**
- All traffic flows through Nginx
- `/api` requests are reverse proxied internally
- Containers communicate through Docker’s internal DNS
- Build stage and runtime stage are separated

---

## 🐳 Run the Project Locally

### 1️⃣ Build the containers

```bash
docker compose build

## 2️⃣ Start the application
   docker compose up

## 3️⃣ Open in browser
   http://localhost

## 🩺 Healthcheck
    GET /health

   
