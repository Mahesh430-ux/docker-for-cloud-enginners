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
