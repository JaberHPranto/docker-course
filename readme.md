## DOCKER BASICS

### Images

Docker Image is a lightweight,standalone, executable package that is required to run a piece of software. It includes all the libraries, tools, runtime for that software.

### Containers

Container is a runnable instance where we run our image. It is completely independent from out host system. It follows the instruction mentioned in the image and executes these to run the application.

So to run the application, we first create a image based on the application environment, tools, runtime etc and create a container based on that image to execute the application.

Image is like recipe for a cake, and container is actual baked cake which is made based on that recipe

### Volumes

Volume is persistent data storage mechanism to share to between a host and a container and/or even across multiple containers or server

### Network

It's a communication channel that can be used to communicate among multiple containers or external world/services.

### Docker Workflow

![docker-workflow](https://pbs.twimg.com/media/F1aC3GaaQAAWazN.jpg:small)

### Dockerfile Basics

Create a file named **Dockerfile** (super important: don't messed up, should have the exact same name)

```
// select a base image for the container.
FROM img[:tag] [as name]
FROM node:20-alpine
FROM ubuntu:20.04

// working directory for the container
WORKDIR /path/to/dir
WORKDIR /app

// copy files from build context to image
COPY src dest
COPY . /app

// execute command in shell during build
CMD <command>
CMD npm run build

// expose port that will listen on that port at runtime
EXPOSE <port> [<port>/<protocol>]
EXPOSE 3000

// set environment variables during build process
ENV KEY=VALUE
ENV NODE_ENV=PRODUCTION

// argument variables are passed during build process
ARG <name>[=<default value>]
ARG NODE_VERSION=20

// for externally mounting volumes
VOLUME ["/data"]
VOLUME /my-volume

```

### Docker Commands

- Shows all the **docker images** of your system

```
docker images
```

- Shows the **docker containers** of your system

```
docker ps (for active containers)
docker ps -a (for all containers)
```

- **Remove** a container

```
docker rm <container-id> --force
```

- **Pulling** an image from docker hub

```
docker pull ubuntu
```

- **Run the image** (-it means in interactive mode). It will create a container based on the image

```
docker run -it ubuntu
```

- Same as previous but will direct put you to the **working directory** of the created container

```
docker run -it ubuntu sh
```

- **Start** the container

```
docker start <container_name or container_id>
```

- **Stop** the container

```
docker stop <container-name or container-id>
```

- **Building** the docker image (-t = tags, by default latest)

```
docker build -t <image-name> <path-to-directory>
```

- **Run** the docker with port mapping

```
docker run -p <container-port>:<host-port> image-name
```

- **Run** the docker with port mapping and volume to reflect changes in code without rebuilding

```
docker run -p <container-port>:<host-port> -v "$(pwd):/app" -v /app/node_modules image-name
```

### Docker Compose

- CLI to automatically generate a docker compose file

```
docker init
```
