Overview

This project is a fully containerized MEAN stack application that performs basic CRUD operations using MongoDB, Express.js, Angular, and Node.js. The application is deployed on an Ubuntu EC2 instance and served via Nginx reverse proxy on port 80. CI/CD is implemented using GitHub Actions to automate image building, pushing, and deployment on changes.

Architecture
Components Used

Frontend: Angular application

Backend: Node.js + Express REST API

Database: MongoDB (Docker container)

Reverse Proxy: Nginx

Infrastructure: Ubuntu EC2 instance

Container Platform: Docker + Docker Compose

CI/CD: GitHub Actions & Docker Hub registry


Architecture Diagram
Developer → GitHub Repo → CI/CD → Docker Hub → EC2 → Docker Compose → Nginx → User

Features

✔ Fully containerized MEAN application
✔ Dockerfiles for frontend and backend
✔ MongoDB containerized or native installation not required
✔ Nginx reverse proxy (application served on port 80)
✔ AWS EC2 deployment
✔ CI/CD via GitHub Actions
✔ Automatic Docker image build + push + deployment
✔ Easy to scale or update


File & Folder Structure
.
├── backend/
├── frontend/
├── nginx/default.conf
├── docker-compose.yml
└── .github/workflows/cicd.yml

Deployment Details
1. Local Deployment
docker compose up -d


Open in browser:

http://65.1.92.247

2. Cloud Deployment (AWS EC2)
Requirements

Ubuntu 22.04 EC2 instance

Ports allowed:

22/tcp for SSH

80/tcp for HTTP

Commands Used on EC2
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
exit


Clone the repository:

git clone https://github.com/<username>/<repo>.git
cd repo
docker compose up -d

Application Access
http://<EC2_PUBLIC_IP>/

CI/CD Workflow

A GitHub Actions pipeline runs automatically on every commit pushed to main.

Pipeline stages:

Checkout latest source code

Build Docker images for frontend and backend

Push images to Docker Hub

SSH into EC2

Pull latest code and images

Restart containers via Docker Compose

You only update code → the deployment updates automatically.

Pipeline file:

.github/workflows/cicd.yml

Docker Commands Used
Build & Push images (handled automatically by CI/CD)
docker build -t <user>/mean-backend:latest backend/
docker build -t <user>/mean-frontend:latest frontend/
docker push <user>/mean-backend:latest
docker push <user>/mean-frontend:latest

Nginx Reverse Proxy

nginx/default.conf routes:

/ → Angular frontend

/api/ → Node backend

Docker Compose Overview

Services included:

Angular frontend

Node backend

MongoDB

Nginx reverse proxy

Command to run:

docker compose up -d

Screenshots to Include (Important)

Include the following screenshots in README:

Infrastructure & Deployment

EC2 running instance with public IP

Terminal docker ps showing 4 containers running

Application

Application UI accessible from browser

CRUD working demo (Create/Delete)

CI/CD

GitHub Actions pipeline run screen (success)

Docker Hub repository page showing images pushed

Docker

Terminal showing docker compose up -d on EC2

Nginx reverse proxy config screenshot (default.conf)

Organize them under a section:

Screenshots

Add them like:

<img width="1914" height="853" alt="Screenshot From 2025-11-28 19-06-53" src="https://github.com/user-attachments/assets/436149b3-c412-4e4e-aff5-c124ce149c2b" />

<img width="1914" height="853" alt="Screenshot From 2025-11-28 19-07-21" src="https://github.com/user-attachments/assets/817f0350-60f7-415b-8586-3b7893fdc7e5" />

...

Optional Improvements

HTTPS via Let’s Encrypt

Autoscaling with ECS/Kubernetes

Terraform infrastructure automation

Multi-stage Angular production build

Conclusion

This project demonstrates:

Docker containerization of a full-stack MEAN application,

Deployment using Docker Compose and Nginx,

Automated build and deployment pipeline using GitHub Actions,

Hosting on AWS EC2 with scalable architecture.

This setup satisfies typical DevOps requirements:
containerization, orchestration, cloud deployment, and CI/CD.
