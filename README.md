# docker-kubernetes

## docker
Images
- An executable application artifact
- Includes app source code, but also complete environment configuration

Containers
- A running instance of an image
- That's when the container environment is created
- It is possible to run multiple containers from 1 image

Docker hub
- world's largest library and community for container images
- contain list of image versioning
- Docker Hub is the default location where docker will look for images

Pull images
- if no version is provided, docker hub will pull the latest version
```bash
docker pull <image>:<version>
```

View images
```bash
docker images
```

Create container
```bash
docker run <image>:<version>
```
- command -d : detach command (runs container in background and prints the container ID)
```bash
docker run -d <image>:<version>
```

Port binding
- command -p : publish command (allocate local host port to the container)
- Example: ```bash docker run -p 6000:6379 redis``` will bind the host port 6000 to the container port 6379 of that container
- Best practices: Standard to use same port on your host as container is using
```bash
docker run -d -p <local-host-port>:<container-port> <image>:<version>
```

Naming container
- command --name: creates a customized container name for the container
```bash
docker run --name <container-name> -d -p <local-host-port>:<container-port> <image>:<version>
```

View container
```bash
docker ps
```
- command -a : Lists all containers (stopped and running)
```bash
docker ps -a
```

View container logs
- view logs from service running inside the container (which are present at the time of execution)
- can use container ID or container name
```bash
docker logs <container ID>
```
```bash
docker logs <container name>
```

Start existing container
```bash
docker start <container ID>
```

Stop container
- we can stop a container based off its container ID or container name
```bash
docker stop <container ID>
```
```bash
docker stop <container name>
```

Build own Docker Images
- Create a "definition" of how to build an image from our application
- Dockerfile is a text document that contains commands to assemble an image
- Docker can then build an image by reading those instructions

Keywords:
FROM : Build this image from the specified image
RUN : Execute any commang in a shell inside the container environment
COPY : copy files or directories from <src> and add them to the filesystem of the container at the path <dest>. While "RUN" is executed in the container, "COPY" is executed in the host
```bash
COPY <src> <dest>
```

WORKDIR : set the working directory for all the following commands
```bash
WORKDIR <directory>
```

Example of a Dockerfile
```bash
FROM node: 19-alpine
COPY src /app/
WORKDIR /app
RUN npm install
```
Build the docker image based on the Dockerfile
command -t : set a name and optionally a tag in the "name:tag" format
```bash
docker build -t <name>:<tag> <location-of-dockerfile>
```
