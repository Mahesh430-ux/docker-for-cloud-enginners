# docker-for-cloud-enginners

🐳 Day 1: Introduction to Docker

📖 What is Docker?

Docker is an open-source containerization platform that allows developers to build, package, and run applications in containers. A container includes everything an application needs, such as code, libraries, dependencies, and configurations, ensuring it runs consistently across different environments.

🚀 Why Docker?
Eliminates the "It works on my machine" problem.
Provides consistent development and production environments.
Makes application deployment faster and easier.
Supports CI/CD and cloud-native applications.
Lightweight compared to Virtual Machines.

* Key Concepts :-
Docker Image: A blueprint used to create containers.
Docker Container: A running instance of a Docker image.
Dockerfile: A text file containing instructions to build a Docker image.
Docker Hub: A cloud-based registry to store and share Docker images.

* Docker Workflow :-

Application Code
       ↓
   Dockerfile
       ↓
 Docker Image
       ↓
Docker Container
       ↓
Deploy Anywhere

* What I Learned Today :-
What Docker is and why it is used.
The difference between Docker Images and Containers.
The role of Dockerfiles and Docker Hub.
How Docker simplifies application deployment across different environments.

* Docker Fundamentals: How Applications Work with Docker 🐳

* Day 2 - Understanding Docker from Scratch that how actually it works :-

Today I learned how Docker works, how a Docker image is created, what a Dockerfile does, how containers run applications, and how Docker helps developers build applications that run consistently on any machine.

* What Problem Does Docker Solve?
Imagine you build a Python application on your laptop.

It works perfectly on your system because you already have:

* Python installed
* Required libraries
* Correct operating system
* Environment variables

But when you send the project to someone else, it may not work because their computer has a different setup.

Docker solves this problem by packaging everything the application needs into one portable package.

Build once, run anywhere.

* How an Application Works :-
Every application follows this basic flow:

User
   │
   ▼
Application Code
   │
   ▼
Programming Language Runtime
(Python / Java / Node.js)
   │
   ▼
Required Libraries
   │
   ▼
Operating System
   │
   ▼
Hardware

Without the required runtime or libraries, the application cannot run.

* What is a Dockerfile?
A Dockerfile is a text file that contains instructions for Docker to build an image.

Think of it as a recipe.
Just like a cooking recipe tells a chef how to prepare food, a Dockerfile tells Docker how to prepare an application.

Example:

dockerfile
FROM python:3.12

WORKDIR /app

COPY . .

RUN pip install flask

CMD ["python", "app.py"]

* Understanding Each Instruction

* FROM

dockerfile
FROM python:3.12

Starts with an official Python image.

This becomes the base environment for the application.

*WORKDIR

dockerfile
WORKDIR /app

Creates a working directory inside the container.
All future commands will execute inside this folder.

 COPY

dockerfile
COPY

Copies the project files from the local machine into the Docker image.

 RUN

dockerfile
RUN pip install flask

Executes commands while building the image.

Here, Docker installs Flask.

* CMD
dockerfile
CMD ["python", "app.py"]

Defines the default command that runs when the container starts.

* 🏗️ How Docker Builds an Image
When we run:
docker build -t myapp

Docker performs these steps

Read Dockerfile
        │
        ▼
Download Base Image
        │
        ▼
Create Working Directory
        │
        ▼
Copy Project Files
        │
        ▼
Install Dependencies
        │
        ▼
Save Everything
        │
        ▼
Docker Image Created

The Docker image now contains:

* Operating System files
* Programming language runtime
* Libraries
* Application code
* Configuration

* What is a Docker Image?
A Docker image is a packaged application that includes everything needed to run the application.

It contains:

* Base operating system
* Runtime
* Libraries
* Application files
* Dependencies

A Docker image is read-only and acts as a blueprint.

* 📦 What is a Docker Container?
A Docker container is a **running instance of a Docker image**.

Relationship:

Dockerfile
      │
      ▼
Docker Image
      │
docker run
      │
      ▼
Docker Container

*One Docker image can create multiple containers.

Docker Image
      │
 ┌────┼────┐
 ▼    ▼    ▼
C1   C2   C3
Each container runs independently.

* How a Container Works :-
When we execute:
docker run myapp

Docker:

1. Reads the Docker image.
2. Creates an isolated environment.
3. Starts the application.
4. Executes the command defined in `CMD`.

The application is now running inside the container.

* Docker Deployment Workflow :-
Write Application Code
          │
          ▼
Create Dockerfile
          │
          ▼
docker build
          │
          ▼
Docker Image
          │
          ▼
docker run
          │
          ▼
Docker Container
          │
          ▼
Test Application
          │
          ▼
Push Image to Docker Hub
          │
          ▼
Deploy on AWS EC2 / ECS / Kubernetes
          │
          ▼
Application Available to Users

*Deploying a Docker Application :-

* Step 1: Build the Image
docker build -t myapp .

* Step 2: Verify Images :-
docker images

* Step 3: Run the Container:-
docker run -p 5000:5000 myapp

The application becomes available on:-
<http://localhost:5000>

* Step 4: View Running Containers :-
docker ps

* Step 5: Stop a Container :-
docker stop <container_id>

* Step 6: Push Image to Docker Hub:-
docker tag myapp username/myapp:v1
docker push username/myapp:v1

* Deploying on AWS EC2

Install Docker:-
sudo dnf install docker -y

Start Docker:
sudo systemctl start docker

Pull the image:
docker pull username/myapp:v1

Run the container:
docker run -d -p 80:5000 username/myapp:v1
Users can now access the application through the EC2 instance.

* Docker in One Picture :-

Application Code
        │
        ▼
Dockerfile
        │
docker build
        │
        ▼
Docker Image
        │
docker run
        │
        ▼
Docker Container
        │
        ▼
Application Running
        │
        ▼
Docker Hub
        │
        ▼
AWS EC2 / ECS / Kubernetes
        │
        ▼
End Users

* Key Takeaways :-
* Docker packages applications with all their dependencies.
* A Dockerfile is a set of instructions to build an image.
* A Docker image is a portable, read-only package.
* A Docker container is a running instance of an image.
* Containers provide isolated environments for applications.
* Docker ensures applications run consistently across different systems.
* Images can be pushed to Docker Hub and deployed on cloud platforms like AWS EC2, Amazon ECS, and Kubernetes.

* 🛠️ Essential Docker Commands

| Command                         | Purpose                       |
| ------------------------------- | ----------------------------- |
| `docker build -t myapp .`       | Build a Docker image          |
| `docker images`                 | List all images               |
| `docker run myapp`              | Start a container             |
| `docker run -p 5000:5000 myapp` | Run with port mapping         |
| `docker ps`                     | View running containers       |
| `docker ps -a`                  | View all containers           |
| `docker stop <container_id>`    | Stop a running container      |
| `docker rm <container_id>`      | Remove a container            |
| `docker rmi <image_id>`         | Remove an image               |
| `docker pull <image>`           | Download an image             |
| `docker push <image>`           | Upload an image to Docker Hub |

Day 3 :-

* Docker Commands - Day 2 (Part 1)
* 1  docker exec
❓What does it do?
The docker exec command allows you to run a command inside an already running container.

Think of it like entering a room (container) that is already occupied, doing some work, and then coming back out.

* 1) docker version`
* What does it do?
Displays the Docker Client and Docker Engine (Server) version installed on your system.

*Syntax
docker version

* Sample Output :-
Client:
 Version: 28.2.2
 API version: 1.51

Server:
 Engine:
  Version: 28.2.2

* Explanation :-
* Client → The Docker CLI that you use to type commands.
* Server (Docker Engine)** → The background service that creates and manages images and containers.
* Version → Shows the installed Docker version.

* When do we use it?
* Verify Docker installation.
* Check compatibility between Client and Server.
* Troubleshoot Docker issues.

* 1) docker info:-
* What does it do?
Displays detailed information about the Docker environment.

* Syntax
docker info

* Sample Output

Containers: 5
 Running: 2
 Stopped: 3
Images: 15
Server Version: 28.2.2
Storage Driver: overlay2
CPUs: 4
Total Memory: 8GB

* Explanation :-
* Containers → Total containers.
* Running → Active containers.
* Stopped → Inactive containers.
* Images → Total Docker images.
* Storage Driver → Storage backend used by Docker.
* CPUs & Memory → Resources available to Docker.

* When do we use it?
* Check Docker status.
* Verify system resources.
* Troubleshoot Docker.

* 4 docker images
* What does it do?
Lists all Docker images stored on your local machine.

* Syntax
docker images

* Sample Output
REPOSITORY   TAG      IMAGE ID       CREATED        SIZE
ubuntu       latest   123abc456def   3 days ago     80MB
nginx        latest   456def789ghi   2 days ago     192MB
myapp        latest   987xyz654abc   5 minutes ago  250MB

* Explanation
* Repository → Image name.
* Tag → Image version.
* Image ID→ Unique identifier.
* Created→ Build/download time.
* Size → Disk usage.
When do we use it?
To check which Docker images are available locally.

* 1) docker image ls:-
What does it do?
Lists all Docker images.

* Syntax
docker image ls

*Output
Same output as:
docker images

* Explanation
`docker image ls` is simply the newer and more descriptive version of `docker images`.

* When do we use it
To view local Docker images.

* 1) docker search :-  
* What does it do?
Searches Docker Hub for available images.

* Syntax
docker search nginx

*Sample Output
NAME               DESCRIPTION
nginx              Official nginx image
bitnami/nginx      Bitnami nginx image
linuxserver/nginx  Community nginx image

*Explanation
Docker searches Docker Hub and displays matching images.

When do we use it :-
Before downloading an image.

* 1) docker pull:-
* What does it do?
Downloads an image from Docker Hub.

* Syntax
docker pull nginx

* Sample Output
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:abcd1234...
Status: Downloaded newer image for nginx:latest

* Explanation
Docker downloads the image and stores it locally.

* When do we use it?
Whenever we need an image that is not already available on our system.

* 8)docker run :-
*What does it do?
Creates a new container from an image and starts it.

* Syntax
docker run nginx

* Sample Output
Container started successfully

(In reality, the container may run in the foreground and show application logs instead of this exact message.)

* Explanation
Docker performs these steps:
Image
  │
  ▼
Create Container
  │
  ▼
Start Container
  │
  ▼
Run Application

*When do we use it?
To launch an application from a Docker image.

* 1) docker ps
*What does it do?
Displays only running containers.

*Syntax
bash
docker ps

* Sample Output
CONTAINER ID   IMAGE    STATUS         PORTS
ab1234cd56ef   nginx    Up 5 minutes   80/tc

* Explanation
Shows active containers only.
📌 When do we use it?

To check which containers are currently running.

1) docker ps -a`
What does it do?
Displays all containers, including stopped ones.

* Syntax
docker ps -a

* Sample Output :-
CONTAINER ID   IMAGE    STATUS
ab1234         nginx    Up 5 minutes
bc5678         ubuntu   Exited (0) 2 hours ago

* Explanation
Shows:
* Running containers
* Stopped containers
* Exited containers

 📌 When do we use it
To view the complete container history.

* 1) docker stop :-
What does it do?
Stops a running container.

Syntax
docker stop <container_id>

* Sample Output
ab1234

*Explanation :-
Docker gracefully stops the container.

When do we use it?
Before removing or restarting a container.

* 1) docker start :-

*What does it do?
Starts a previously stopped container.

* Syntax
docker start <container_id>

*Sample Output
ab1234

Explanation:-
The existing container starts again without creating a new one.

*When do we use it?
To reuse an existing stopped container.
Docker restart
What does it do?

Stops and immediately starts a container.

*Syntax
docker restart <container_id>

* Sample Output
ab1234

 Explanation
Equivalent to:
docker stop <container_id>
docker start <container_id>

* When do we use it?
After changing application settings or if the application becomes unresponsive.

* 1) docker rm
* What does it do?
Removes a stopped container.

*Syntax :-
docker rm <container_id>

*Sample Output :-
ab1234
*Explanation:-
The container is permanently deleted from the system.

* When do we use it?
To clean up unused containers.

* 1) docker rmi
*What does it do?
Deletes a Docker image.

* Syntax :-
docker rmi nginx

* Sample Output :-
Untagged: nginx:latest
Deleted: sha256:abcd1234...

 Explanation :-
The image is removed from local storage.

* When do we use it?
To free up disk space by deleting unused images.

* 1) docker logs
* ❓What does it do?
Displays logs generated by a container.

* Syntax
docker logs <container_id>

 Sample Output ;-
Application Started...
Database Connected...
Server Listening on Port 5000...

* Explanation:-
Shows everything the application has printed since the container started.

* When do we use it?
To debug errors and monitor application activity.

---

* Quick Revision Table

| Command           | Purpose                                     |
| ----------------- | ------------------------------------------- |
| `docker version`  | Display Docker Client and Server versions   |
| `docker info`     | Show Docker environment details             |
| `docker images`   | List all local Docker images                |
| `docker image ls` | List local images (same as `docker images`) |
| `docker search`   | Search Docker Hub for images                |
| `docker pull`     | Download an image from Docker Hub           |
| `docker run`      | Create and start a new container            |
| `docker ps`       | Show running containers                     |
| `docker ps -a`    | Show all containers                         |
| `docker stop`     | Stop a running container                    |
| `docker start`    | Start a stopped container                   |
| `docker restart`  | Restart a container                         |
| `docker rm`       | Remove a stopped container                  |
| `docker rmi`      | Remove an image                             |
| `docker logs`     | View container logs                         |

Day 4 :-

1. Enter a Running Container
docker exec -it mycontainer /bin/bash
What it does: Opens a terminal inside the running container.

2. View Container Logs
docker logs mycontainer
What it does: Displays everything the application has printed.

3. View Live Logs
docker logs -f mycontainer
What it does: Continuously shows new logs as they are generated.

4. Inspect Container
docker inspect mycontainer
What it does: Shows detailed information like IP address, mounts, ports, and environment variables.

5. Check Resource Usage
docker stats
What it does: Displays live CPU, memory, network, and disk usage of running containers.

6. View Running Processes
docker top mycontainer
What it does: Shows processes running inside the container.

7. Check Port Mapping
docker port mycontainer
What it does: Displays which host ports are connected to container ports.

8. Rename a Container
docker rename old_name new_name
What it does: Changes the name of an existing container.

9. Copy File to Container
docker cp notes.txt mycontainer:/tmp/
What it does: Copies a file from your computer into the container.

10. Copy File from Container
docker cp mycontainer:/tmp/output.txt .
What it does: Copies a file from the container to your current directory.

11. Export a Container
docker export mycontainer > container.tar
What it does: Saves the container's filesystem as a .tar archive.

12. Import a Container
docker import container.tar myimage
What it does: Creates a Docker image from an exported container.

13. Save an Image
docker save -o nginx.tar nginx
What it does: Saves a Docker image to a tar file for backup or transfer.

14. Load an Image
docker load -i nginx.tar
What it does: Restores a previously saved Docker image.
. Check File Changes
docker diff mycontainer
What it does: Shows which files were added (A), changed (C), or deleted (D) inside the container
