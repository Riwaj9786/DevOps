# Docker:

## 1. Docker Desktop:
- Docker Desktop comes pre-bundled with Docker Engine, Docker Compose, Kubernetes amongst others.

Check if Docker Engine and Docker Compose are installed correctly on the local machine by writing the command on the terminal:
a. To check the Docker Engine version:
  docker --version

b. To check the Docker Compose version:
  docker-compose --version


## 2. Dockerfile:
- A dockerfile is a text file that contains instructions, at times called commands or directives, which dictate how to create a Docker image.
- In short, Docker files are blueprints for creating images.

## 3. Docker Image:
- An image is basically a read only template with instructions for creating a Docker container.
- Often, an image is based on another image, with some additional customization.
For example: You may build an image which is based on the Ubuntu image, but install the Apache web server and your application as well as the configuration details needed to make your application run.

## 4. Container:
- A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI.
- We can connect a container to one or more networks attached storage to it, or even create a new image based on its current state.
