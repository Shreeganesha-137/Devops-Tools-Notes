## Docker: Complete Guide

### **What is Docker?**
Docker is a containerization platform that allows developers to package applications and their dependencies into lightweight, portable containers. Containers ensure that applications run consistently across different environments.

### **Why Use Docker?**
1. **Portability:** Run anywhere (local, cloud, servers).
2. **Scalability:** Easily scale applications with container orchestration tools.
3. **Consistency:** Avoid environment-specific issues.
4. **Resource Efficiency:** Containers use fewer resources than virtual machines.
5. **Faster Deployment:** Containers start quickly and reduce downtime.

---

## **Key Docker Concepts**

### **1. Docker Images**
- A Docker image is a lightweight, stand-alone, executable package that includes everything needed to run a piece of software (code, libraries, dependencies, and configuration files).
- Images are built from Dockerfiles and stored in **Docker Hub**.

**Common Commands:**
```sh
# List all downloaded images
docker images

# Pull an image from Docker Hub
docker pull ubuntu:latest

# Remove an image
docker rmi image_id
```

### **2. Docker Containers**
- A container is a running instance of a Docker image.
- Containers are isolated environments, ensuring that applications run consistently.

**Common Commands:**
```sh
# Run a container
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# Stop a container
docker stop container_id

# Remove a container
docker rm container_id
```

### **3. Dockerfile**
- A Dockerfile is a script that contains a set of instructions for building a Docker image.

**Example Dockerfile:**
```Dockerfile
# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package.json .
RUN npm install

# Copy the project files
COPY . .

# Expose a port and start the application
EXPOSE 3000
CMD ["node", "index.js"]
```

**Build and Run the Image:**
```sh
# Build an image
docker build -t myapp .

# Run the container
docker run -p 3000:3000 myapp
```

### **4. Docker Compose**
- Docker Compose allows you to define multi-container applications.

**Example `docker-compose.yml`:**
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  database:
    image: mysql
    environment:
      MYSQL_ROOT_PASSWORD: password
```

**Commands:**
```sh
# Start services
docker-compose up -d

# Stop services
docker-compose down
```

### **5. Docker Hub**
- A cloud-based registry to store and share Docker images.
- You can push your own images to Docker Hub for sharing.

```sh
# Log in to Docker Hub
docker login

# Push an image to Docker Hub
docker tag myapp username/myapp

docker push username/myapp
```

---

## **Real-World Scenario**
### **Scenario: Deploying a Web Application with Docker**
1. A developer writes a web application in Node.js.
2. They create a `Dockerfile` to containerize the app.
3. They build a Docker image using `docker build`.
4. The image is pushed to Docker Hub.
5. A team member pulls the image and runs it locally.
6. The image is deployed to a cloud server using `docker run`.
7. Updates are made, a new image is built, and the cycle repeats.


# Docker Entry-Level Questions and Answers

## 1. What is Docker?
**Answer:** Docker is an open-source platform that enables developers to automate the deployment of applications inside lightweight, portable containers.

## 2. What is a Docker Container?
**Answer:** A Docker container is a lightweight, standalone, and executable package that includes everything needed to run an application, such as code, runtime, libraries, and dependencies.

## 3. What is a Docker Image?
**Answer:** A Docker image is a lightweight, stand-alone, and executable software package that contains all the dependencies and instructions needed to run an application in a container.

## 4. How do you create a Docker container?
**Answer:** You can create a Docker container using the command:
```bash
docker run -d --name my_container my_image
```

## 5. How do you list all running Docker containers?
**Answer:** Use the command:
```bash
docker ps
```

## 6. How do you list all Docker containers, including stopped ones?
**Answer:** Use the command:
```bash
docker ps -a
```

## 7. How do you stop a running Docker container?
**Answer:** Use the command:
```bash
docker stop <container_id>
```

## 8. How do you remove a Docker container?
**Answer:** Use the command:
```bash
docker rm <container_id>
```

## 9. How do you remove a Docker image?
**Answer:** Use the command:
```bash
docker rmi <image_id>
```

## 10. What is a Dockerfile?
**Answer:** A Dockerfile is a script containing a series of instructions that are used to build a Docker image.

## 11. How do you build a Docker image?
**Answer:** Use the command:
```bash
docker build -t my_image .
```

## 12. What is the difference between CMD and ENTRYPOINT in Docker?
**Answer:** CMD sets default commands and arguments, while ENTRYPOINT is used to define a fixed command that cannot be overridden easily.

## 13. How do you run a Docker container interactively?
**Answer:** Use the command:
```bash
docker run -it my_image bash
```

## 14. How do you check the logs of a running container?
**Answer:** Use the command:
```bash
docker logs <container_id>
```

## 15. How do you restart a stopped container?
**Answer:** Use the command:
```bash
docker start <container_id>
```

## 16. How do you inspect a container?
**Answer:** Use the command:
```bash
docker inspect <container_id>
```

## 17. What is a Docker Volume?
**Answer:** A Docker Volume is a persistent storage mechanism that allows data to persist beyond the lifecycle of a container.

## 18. How do you create a Docker Volume?
**Answer:** Use the command:
```bash
docker volume create my_volume
```

## 19. How do you attach a volume to a container?
**Answer:** Use the command:
```bash
docker run -v my_volume:/data my_image
```

## 20. What is Docker Compose?
**Answer:** Docker Compose is a tool for defining and running multi-container Docker applications using a YAML file.

## 21. How do you start services using Docker Compose?
**Answer:** Use the command:
```bash
docker-compose up -d
```

## 22. How do you stop services using Docker Compose?
**Answer:** Use the command:
```bash
docker-compose down
```

## 23. What is the default network driver in Docker?
**Answer:** The default network driver in Docker is **bridge**.

## 24. How do you remove all stopped containers?
**Answer:** Use the command:
```bash
docker container prune
```

## 25. How do you remove all unused Docker images?
**Answer:** Use the command:
```bash
docker image prune
```
For More Questions Pls refer -> [https://www.geeksforgeeks.org/docker-interview-questions/](Docker-Interview)