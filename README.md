# Docker Two-Tier Flask Application

## Project Overview

This project demonstrates how to containerize and deploy a two-tier application using Docker.

The application consists of:

* Flask Web Application (Frontend/Backend)
* MySQL Database
* Docker Network for container communication
* Docker Volume for persistent storage
* Multi-Stage Docker Build
* Docker Compose for orchestration

The project was implemented and tested on an AWS EC2 Ubuntu server.

---

## Architecture

```text
+------------------+
|   Flask App      |
|   Port : 5000    |
+---------+--------+
          |
          |
          v
+------------------+
|      MySQL       |
|   Port : 3306    |
+------------------+
```

---

## Technologies Used

* Docker
* Docker Compose
* Python Flask
* MySQL
* Linux (Ubuntu EC2)
* AWS EC2


# Implementation Steps

## 1. Clone Repository and Review Project Structure

![Project Structure](screenshots/01_project_structure.png)

---

## 2. Create Dockerfile

Created a Dockerfile to containerize the Flask application.

![Dockerfile Created](screenshots/02_dockerfile_created.png)

---

## 3. Build Docker Image

Built the Flask application image.

```bash
docker build -t flask-app:v1 .
```

![Docker Image Built](screenshots/03_docker_image_built.png)

---

## 4. Create Custom Docker Network

Created a dedicated network for communication between Flask and MySQL containers.

```bash
docker network create twotier
```

![Custom Network Created](screenshots/04_custom_network_created.png)

---

## 5. Create Docker Volume

Created a persistent volume for MySQL data storage.

```bash
docker volume create mysql-data
```

![MySQL Volume Created](screenshots/05_mysql_volume_created.png)

---

## 6. Run MySQL Container

Started the MySQL database container.

![MySQL Container Running](screenshots/06_mysql_container_running.png)

---

## 7. Run Flask Container

Started the Flask application container and connected it to the Docker network.

![Flask Container Running](screenshots/07_flask_container_running.png)

---

## 8. Access Application in Browser

Verified that the application is accessible through the browser.

![Application Running](screenshots/08_application_running_in_browser.png)

---

## 9. Verify Data Storage in MySQL

Inserted data from the application and verified it inside the MySQL database.

![Data Stored in MySQL](screenshots/09_data_stored_in_mysql.png)

---

## 10. Verify Volume Persistence

Deleted containers and recreated them using the same Docker volume.

Verified that MySQL data persisted successfully.

![Volume Persistence Verified](screenshots/10_volume_persistence_verified.png)

---

## 11. Inspect Docker Network

Inspected the Docker network and verified container connectivity.

```bash
docker network inspect twotier
```

![Network Inspect](screenshots/11_network_inspect.png)

---

## 12. Create Multi-Stage Dockerfile

Created a multi-stage Docker build to optimize image size and improve security.

![Multi-Stage Dockerfile](screenshots/12_multistage_dockerfile_created.png)

---

## 13. Build Multi-Stage Image and Compare Sizes

Built the optimized image and compared image sizes.

![Image Size Comparison](screenshots/13_multistage_image_built_and_image_size_comparison.png)

---

## 14. Run Multi-Stage Container

Verified that the optimized image runs successfully.

![Multi-Stage Container Running](screenshots/14_multistage_container_running.png)

---

## 15. Create Docker Compose Configuration

Created a docker-compose.yml file to manage the complete application stack.

![Docker Compose Created](screenshots/15_docker_compose_created.png)

---

## 16. Deploy Application Using Docker Compose

Started the application stack using Docker Compose.

```bash
docker compose up -d --build
```

![Docker Compose Running](screenshots/16_docker_compose_up_and_ps.png)

---

## 17. Troubleshooting and Fix

While deploying with Docker Compose, the Flask container initially failed because MySQL was not fully ready when Flask attempted to connect.

Resolved the issue by adding a restart policy and redeploying the stack.

This simulates a real-world troubleshooting scenario.

![Application Logs After Fix](screenshots/17_application_logs_after_fix.png)

---

# Key Docker Concepts Demonstrated

* Docker Images
* Docker Containers
* Dockerfile
* Multi-Stage Builds
* Docker Networks
* Container Communication
* Docker Volumes
* Data Persistence
* Environment Variables
* MySQL Containerization
* Flask Containerization
* Docker Compose
* Troubleshooting Container Startup Issues

---

# Commands Used

## Build Image

```bash
docker build -t flask-app:v1 .
```

## Create Network

```bash
docker network create twotier
```

## Create Volume

```bash
docker volume create mysql-data
```

## Run MySQL Container

```bash
docker run -d --name mysql --network twotier -v mysql-data:/var/lib/mysql -e MYSQL_DATABASE=mydb -e MYSQL_ROOT_PASSWORD=admin -p 3306:3306 mysql:5.7
```

## Run Flask Container

```bash
docker run -d --name flaskapp --network twotier -e MYSQL_HOST=mysql -e MYSQL_USER=root -e MYSQL_PASSWORD=admin -e MYSQL_DB=mydb -p 5000:5000 flask-app:v1
```

## Deploy with Docker Compose

```bash
docker compose up -d --build
```

---

# Learning Outcomes

Through this project, I gained hands-on experience with:

* Building Docker images
* Running multi-container applications
* Managing Docker networks and volumes
* Implementing multi-stage builds
* Using Docker Compose
* Troubleshooting container startup dependencies
* Deploying applications on AWS EC2

---

## Author

**Sriram Ganesh**


