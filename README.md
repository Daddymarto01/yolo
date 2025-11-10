# Overview 
This repository contains a full-stack web application (frontend + backend) built with modern web technologies, orchestrated via Docker, and deployed using Vagrant + Ansible.  
The aim is to demonstrate a production-ready infrastructure workflow: development → containerisation → deployment.

# Requirements
Before starting the containerization, you need to install Docker. Docker consists of three main components: Docker Engine (the core runtime for building and running containers), Docker CLI (the command-line interface for interacting with Docker), and Docker Compose (a tool for defining and running multi-container applications, now integrated as a CLI plugin).

Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 
- Download Docker Desktop from https://www.docker.com/products/docker-desktop (includes Engine, CLI, and Compose plugin) for Windows/Mac.
- For Ubuntu/Linux: from terminal Run sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin.
- Verify installation:from terminal Run docker version (checks Engine/CLI) and docker compose version (checks Compose).

![alt text](image-1.png)

Confirm the version on docker compose.
- Run docker compose version

![alt text](image-2.png)
# Key Features

- Frontend: Built with HTML, CSS and JavaScript (SPA or dynamic UI)  
- Backend: RESTful API (or server-side application) serving the frontend and data endpoints  
- Containerisation: Each service runs in its own Docker container  
- Infrastructure as Code:
  - `Vagrantfile` for provisioning local development VM 
  - `Ansible` playbook/inventory for configuration management  
  - `docker-compose.yaml` for orchestration  
  - Kubernetes (or YAML deployment) manifests for backend & frontend in production  
- Multi-service architecture with roles separation (see `roles/` folder)  
- Clean structure for both client & server, enabling independent development and CI/CD readiness  

## 📁 Repository Structure  
/
├── .vscode/ # VS Code settings
├── backend/ # Backend application code
├── client/ # Frontend application code
├── roles/ # Ansible roles (e.g., webserver, database)
├── docker-compose.yaml # Compose file for multi-container setup
├── frontend-deployment.yaml # Deployment manifest for frontend
├── backend-deployment.yaml # Deployment manifest for backend
├── Vagrantfile # Virtual machine definition for local dev
├── hosts # Inventory of servers
├── inventory.yml # Ansible inventory
├── playbook.yml # Ansible playbook
├── ansible.cfg # Ansible configuration
├── .dockerignore # Docker ignore file
├── .gitignore # Git ignore file
└── README.md # This file
## How to launch the application 
 - Check if any docker containers are running by running docker ps and docker ps -a to check previously launched but stopped containers.
![alt text](image-3.png)\
 - Stop any unnecessary containers and then check again by running docker ps

![alt text](image-4.png)

- Now build your application by running command docker compose build on your terminal. This will install all dependancies including updating nuget package manager.
- Note, faster internet speeds up the building of the project.
![alt text](image-5.png)
- Launch application by running command docker compose up.
- The result will be as show below.
![alt text](image-6.png)

## Confirm that the application is up and running.
- Follow the link shown above http://localhost:3000 to launch the application. 

![alt text](image-7.png)

The above screen is a confirmation that application is running as expected. 
## Check and confirm that the containers are running and that the database (mongo db) is pulled.
- Run command docker ps to list the containers that are running a 
![alt text](image-8.png)
- The resuls are as show above.

## Volumes and Networks: Listing and Inspecting
### Network
Networks enable comms (same network for hostname resolution). List: docker network ls. Inspect: docker network inspect yolo-net (IPs, containers). We use same network for backend to reach mongo.
If logged in as sudo, you could list netwoks by running docker network ls command. If not, add the word sudo at the begining as shown below. 

![alt text](image-9.png)

This shows the networks available and yolo_app_net is our network.
- Copy the Network ID and run sudo docker network inspect to show details on the container network configuration. 

![alt text](image-10.png)
The results will be as shown above.

### Volumes
Volumes persist data. List: docker volume ls. Inspect: docker volume inspect yolo_app-mongo-data (mountpoint: /var/lib/docker/volumes/app-mongo-data/_data).
- Run docker volume ls or sudo docker volume ls to confirm our volume. 

![alt text](image-11.png)

Image above shows yolo_app-mondo-data as our volume. 

- To inspect our volume, copy the volume name and run sudo docker volume inspect yolo_app-mongo-data.

![alt text](image-12.png)

Image above shows volume inspection.