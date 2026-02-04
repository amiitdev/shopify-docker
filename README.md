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

```
Browser
   ↓
Nginx (Port 80 / 443)
   ↓
/api Reverse Proxy
   ↓
Backend (Internal Docker Network)
```

---

## 🔐 Key Design Decisions

- Backend port is **NOT exposed publicly**
- All traffic flows through Nginx
- `/api` requests are reverse proxied internally
- Containers communicate using Docker internal DNS
- Build stage and runtime stage are separated

---

## 🐳 Run the Project Locally

### 1️⃣ Build the containers

```bash
docker compose build
```

### 2️⃣ Start the application

```bash
docker compose up
```

### 3️⃣ Open in browser

```
http://localhost
```

---

## 🩺 Healthcheck

Backend includes a health endpoint:

```http
GET /health
```

Docker automatically monitors container health.

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

docker-compose.yml
```

---

## 🎯 What This Project Demonstrates

- Docker multi-stage builds
- Reverse proxy architecture
- Internal container networking
- Production-style deployment setup
- SSH-based Git configuration

---

## 👨‍💻 Author

Amit Kumar  
DevOps / Fullstack Developer
