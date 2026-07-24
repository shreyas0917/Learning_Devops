# Day 36 – Dockerize a Full Stack Application

## Project Overview

For Day 36 of the #90DaysOfDevOps challenge, I Dockerized my **Modern URL Shortener** application from end to end. The objective was to containerize every component, orchestrate services using Docker Compose, and deploy the application in a production-like environment.

Unlike a simple containerization exercise, this project involved a complete multi-container architecture consisting of a frontend, backend, database, and cache, all communicating through a custom Docker network.

---

# Application Chosen

**Project:** Modern URL Shortener

### Why I Chose This Project

I selected this project because it represents a real-world full-stack application with multiple dependent services. It allowed me to practice production-ready Docker concepts such as:

- Multi-stage Docker builds
- Non-root containers
- Docker Compose orchestration
- Persistent volumes
- Health checks
- Environment variable management
- Custom Docker networking
- Cloud deployment on AWS EC2
- Docker Hub image publishing

---

# Project Architecture

```
                 Browser
                     │
                     ▼
          Nginx (React Frontend)
                     │
                     ▼
        Express.js Backend API
              │             │
              ▼             ▼
        MongoDB         Redis Cache
```

All services are connected through a custom Docker bridge network using Docker Compose.

---

# Dockerfile Highlights

## Frontend

- Multi-stage build
- Node.js build stage
- Nginx runtime image
- Optimized static asset serving

## Backend

- Multi-stage build
- Node.js Alpine base image
- Non-root user
- Production dependencies only
- Lightweight runtime image

---

# Docker Compose Features

Implemented a production-style Docker Compose configuration including:

- Frontend service
- Backend service
- MongoDB service
- Redis service
- Persistent MongoDB volume
- Custom bridge network
- Environment variable support using `.env`
- MongoDB health checks
- Redis health checks
- Automatic service restart policy

---

# Challenges Faced

## 1. Docker Image Optimization

Initially, the backend image size was significantly larger than expected.

### Solution

- Switched to Alpine base images
- Used multi-stage builds
- Installed only production dependencies
- Removed unnecessary build artifacts

---

## 2. Service Communication

Containers were unable to communicate using localhost.

### Solution

Configured Docker Compose networking and updated environment variables to use service names instead of localhost.

Example:

```
MONGODB_URI=mongodb://mongodb:27017/urlshortener
REDIS_HOST=redis
```

---

## 3. Database Readiness

Backend attempted to connect before MongoDB became available.

### Solution

Implemented Docker Compose health checks and `depends_on` conditions to ensure proper startup order.

---

## 4. AWS Deployment

While deploying on AWS EC2, application ports and Docker networking required additional configuration.

### Solution

- Configured Security Groups
- Exposed required ports
- Built and deployed containers successfully
- Verified application accessibility through the EC2 public IP

---

# Docker Hub

Successfully published production-ready Docker images.

Backend:

```
shreyas17082004/modern-url-shortener-backend:v1
```

Frontend:

```
shreyas17082004/modern-url-shortener-frontend:v1
```

Docker Hub Profile:

https://hub.docker.com/u/shreyas17082004

---

# Final Image Sizes

| Image | Size |
|--------|------|
| Frontend | ~74 MB |
| Backend | ~312 MB |

---

# Technologies Used

- Docker
- Docker Compose
- React
- Node.js
- Express.js
- MongoDB
- Redis
- Nginx
- AWS EC2
- Docker Hub

---

# Learning Outcomes

Through this project, I gained practical experience with:

- Writing production-ready Dockerfiles
- Multi-stage image builds
- Docker Compose orchestration
- Docker networking
- Persistent storage
- Health checks
- Environment variable management
- Docker image optimization
- Publishing images to Docker Hub
- Deploying containerized applications on AWS EC2

---

# Repository

GitHub Repository

> https://github.com/shreyas0917/Modern_URL_Shortener

---

# Result

Successfully Dockerized and deployed a complete full-stack application with a production-style architecture. The project can be pulled directly from Docker Hub and executed using Docker Compose, providing a consistent and reproducible development and deployment environment.

---

#90DaysOfDevOps  
#DevOpsKaJosh  
#TrainWithShubham  
#Docker  
#DockerCompose  
#AWS  
#Nginx  
#MongoDB  
#Redis  
#React  
#NodeJS