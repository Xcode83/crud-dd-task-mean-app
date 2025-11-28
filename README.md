MEAN CRUD Application – Docker, Nginx, Docker Compose & CI/CD Deployment
Overview

This project is a fully containerized MEAN (MongoDB, Express, Angular, Node.js) CRUD application deployed on an Ubuntu EC2 instance using Docker, Docker Compose, and Nginx. The repository also includes a CI/CD pipeline using GitHub Actions that builds and pushes Docker images to Docker Hub and deploys the updated application automatically to the EC2 server.

This assignment demonstrates hands-on experience with containerization, cloud deployment, reverse proxy configuration, and automated CI/CD workflows.

Project Architecture
Browser → Nginx (Reverse Proxy) → Angular Frontend → Node.js Backend → MongoDB


Services involved:

Angular Frontend (Docker)

Node.js Backend API (Docker)

MongoDB Database (Official Docker image)

Nginx Reverse Proxy on port 80 (Docker)

Deployment on Ubuntu EC2

CI/CD using GitHub Actions

Technology Stack

Angular

Node.js / Express.js

MongoDB

Docker & Docker Compose

Nginx

AWS EC2 (Ubuntu 22.04)

Docker Hub

GitHub Actions CI/CD

Repository Structure
backend/
frontend/
nginx/
docker-compose.yml
.github/workflows/cicd.yml
README.md

Docker Images

Both application components are containerized and available on Docker Hub:

docker.io/biswajitop/mean-backend:latest
docker.io/biswajitop/mean-frontend:latest

Run Locally (Development or Testing)
git clone <this-repo-url>
cd <project-folder>
docker compose up -d


Open in browser:

http://localhost/


Stop containers:

docker compose down

Cloud Deployment (Ubuntu EC2)
1. Install Docker and Docker Compose
sudo apt update -y
sudo apt install -y ca-certificates curl gnupg git
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu


Re-login and verify:

docker --version
docker compose version

2. Clone the repo
cd /opt
sudo mkdir mean-app
sudo chown ubuntu:ubuntu mean-app
cd mean-app
git clone <your-repo-url> .

3. Deploy the stack
docker compose up -d
docker ps

4. Access Application
http://<EC2_PUBLIC_IP>/


This exposes the entire UI over port 80 through Nginx.

Nginx Reverse Proxy Overview

The container runs with a reverse proxy that routes traffic:

/         → Angular frontend
/api/     → Node.js backend


Example configuration:

location / {
    proxy_pass http://frontend:4200;
}

location /api/ {
    proxy_pass http://backend:8080;
}

CI/CD Pipeline (GitHub Actions)

This repository contains a GitHub Actions workflow that:

Builds latest frontend and backend Docker images

Pushes images to Docker Hub

SSH into the EC2 instance

Pulls latest images and restarts containers

Required GitHub Secrets
Name	Description
DOCKERHUB_USERNAME	Docker Hub username
DOCKERHUB_TOKEN	Docker Hub token or password
SSH_HOST	EC2 public IP
SSH_USER	SSH username (ubuntu)
SSH_KEY	Private SSH key

The CI/CD config file is located at:

.github/workflows/cicd.yml
