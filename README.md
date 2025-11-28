# Discover Dollar DevOps Assignment – MEAN CRUD App

## 1. Project Overview

This project is a **Dockerized MEAN (MongoDB, Express, Angular, Node.js) CRUD application** deployed on an **AWS EC2 Ubuntu instance** using **Docker Compose** and **Nginx** as a reverse proxy.  

A **GitHub Actions CI/CD pipeline** automatically:

- Builds frontend & backend Docker images
- Pushes images to Docker Hub (`shashwat292/mean-frontend`, `shashwat292/mean-backend`)
- SSHs into the EC2 VM
- Pulls the latest images and restarts containers

**Live URL:** `http://34.204.183.25/` (HTTP on port 80)

---

## 2. Tech Stack

- **Frontend:** Angular 15, served via Nginx inside container
- **Backend:** Node.js, Express, Mongoose
- **Database:** MongoDB (Docker container)
- **Reverse Proxy:** Nginx on EC2 (port 80)
- **Containerization:** Docker, Docker Compose
- **CI/CD:** GitHub Actions + Docker Hub
- **Cloud:** AWS EC2 (Ubuntu 24.04)

---

## 3. Architecture

**Services:**

- `frontend`  
  - Image: `shashwat292/mean-frontend:latest`  
  - Runs Angular build served by Nginx  
  - Exposes port `80` inside container → mapped to host `4200`

- `backend`  
  - Image: `shashwat292/mean-backend:latest`  
  - Node.js + Express + Mongoose REST API  
  - Uses `MONGO_URL=mongodb://mongo:27017/bezkoder_db`  
  - Exposes port `8080` inside container → mapped to host `8081`

- `mongo`  
  - Image: `mongo:6.0`  
  - Data stored in named volume `mongo_data`

- `nginx` (host-level, not in compose)  
  - Listens on port **80**  
  - Proxies:
    - `/` → `frontend` on `127.0.0.1:4200`
    - `/api/` → `backend` on `127.0.0.1:8081/api/`

---

## 4. Local Setup and Run (with Docker)

### Prerequisites

- Docker
- Docker Compose

### Steps

```bash
git clone https://github.com/shashwat-81/discover-dollar-devops-assignment.git
cd discover-dollar-devops-assignment

docker compose up -d
docker compose ps
