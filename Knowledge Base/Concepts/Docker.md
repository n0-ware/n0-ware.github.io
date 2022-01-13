# Docker

## Description
"Docker" generally refers to a compute solution known as a "container." Containers are an excellent choice for deploying infrastructure to their lightweight and cross-functionality via baked-in dependencies. Containers in Docker are essentially `.tar` files that contain all the information the container needs to run. 

Containers are stored in "registries." Running `docker images` on a local system will return the information related to any containers on the system that `docker` knows about. The container itself can be referenced using the name or tag.
- Repository (Name)
- Tag
- Image ID
- Created
- Size


Once an image is built, running the container image will always result in the same configuration state as specified at build-time. This is a great benefit for the software development lifecycle, ensuring that a packaged image runs as expected on any system prepared to run Docker and with the necessary resources. The application is essentially "frozen" in time. 

The `Dockerfiles` that make up an image are a set of "new-line separated" instructions that tell the Docker daemon how to create the image. 

## Installation
### Kali
```
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker --now

## To add yourself to the docker group to use without sudo
sudo usermod -aG docker $USER
```

## AWS-ECR

Containers are stored on AWS in a service called [Elastic Container Registry (ECR)](https://aws.amazon.com/ecr/). These containers can be made available publicly or privately. 

Docker images can be obtained remotely via AWS with the command:
```
docker pull public.ecr.<CONTAINER_ADDRESS>:<tag>
```

Run and interact with a docker container with a similar command:
```
docker run -it public.ecr.<CONTAINER_ADDRESSS>:<TAG>
```

Once inside a container, you may interact with it based on the operating system it is running. 

## Vulnerabilities

### Artifacts
The problem with Docker containers is that artifacts can be left behind that were not intended, items such as
- Passwords and API Keys
	- Check inside config files, profiles, and environment variables (`printenv`)

### Dockerfile
Various layers in the Dockerfile can have vulnerabilities inside them as well depending on the type of information contained in the image or inside the layers. 

### Container Images
See [container images](Container%20Images.md)
