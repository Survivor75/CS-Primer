## Docker Cheat Sheet

## Introduction

Docker is a platform to develop, deploy, and run applications inside containers. Docker is essentially synonymous with containerization.

## Concepts

**Virtual Machines**

Virtual machines are the precursors to Docker containers. Virtual machines also isolate an application and its dependencies. However, Docker containers are superior to virtual machines because they take fewer resources, are very portable, and are faster to spin up.

**Docker Image**

Docker images are more like blueprints, cookie cutters, or molds. Images are the immutable master template that is used to pump out containers that are all exactly alike.

An image contains the Dockerfile, libraries, and code your application needs to run, all bundled together.

**Dockerfile**

A  Dockerfile is a file with instructions for how Docker should build your image.

The Dockerfile refers to a base image that is used to build the initial image layer. 

Additional layers can then be stacked on top of the base image layers, according to the instructions in the Dockerfile. For example, a Dockerfile for a machine learning application could tell Docker to add NumPy, Pandas, and Scikit-learn in an intermediate layer.

Finally, a thin, writable layer is stacked on top of the other layers according to the Dockerfile code.

**Docker Container**

A Docker image plus the command  `docker run image_name`  creates and starts a container from an image.

**Container Registry**

If you want other people to be able to make containers from your image, you send the image to a container registry.  [Docker Hub](https://hub.docker.com/)  is the largest registry and the default.

## Docker Ecosystem Terms

[**Docker Engine**](https://www.docker.com/products/docker-engine)  is the client-server application.

[**Docker Client**](https://docs.docker.com/engine/docker-overview/) is the primary way you’ll interact with Docker. When you use the [Docker Command Line Interface (CLI)](https://docs.docker.com/engine/reference/commandline/cli/) you type a command into your terminal that starts with `docker`. Docker Client then uses the Docker API to send the command to the Docker Daemon.

![Docker-Overview](https://docs.docker.com/engine/images/architecture.svg)

[**Docker Daemon**](https://docs.docker.com/engine/docker-overview/)  is the Docker server that listens for Docker API requests. The Docker Daemon manages images, containers, networks, and volumes.

[**Docker Volumes**](https://docs.docker.com/storage/volumes/) are the best way to store the persistent data that your apps consume and create.  We’ll have more to say about Docker Volumes in Part 5 of this series. Follow me to make sure you don’t miss it.

A  [**Docker Registry**](https://hub.docker.com/)  is the remote location where Docker Images are stored.  You push images to a registry and pull images from a registry. You can host your own registry or use a provider’s registry. For example,  [AWS](https://aws.amazon.com/ecr/)  and  [Google Cloud](https://cloud.google.com/container-registry/)  have registries.

[**Docker Hub**](https://hub.docker.com/)  is the largest registry of Docker images. It’s also the default registry. You can find images and store your own images on Docker Hub for free.

A  [**Docker Repository**](https://docs.docker.com/docker-hub/repos/) is a collection of Docker images with the same name and different tags. The _tag_ is the identifier for the image.

## Scaling Docker

The following four concepts relate to using multiple containers at once.

[**Docker Networking**](https://docs.docker.com/engine/tutorials/networkingcontainers/)  allows you to connect Docker containers together. Connected Docker containers could be on the same host or multiple hosts. For more information on Docker networking, see  [this post](https://www.oreilly.com/learning/what-is-docker-networking).

[**Docker Compose**](https://docs.docker.com/compose/)  is a tool that makes it easier to run apps that require multiple Docker containers. Docker Compose allows you to move commands into a  `docker-compose.yml`  file for reuse. The Docker Compose command line interface (cli) makes it easier to interact with your multi-container app. Docker Compose comes free with your installation of Docker.

[**Docker Swarm**](https://docs.docker.com/engine/swarm/)  is a product to orchestrate container deployment. The  [official Docker tutorial](https://docs.docker.com/get-started/#recap-and-cheat-sheet)  has you using Docker Swarm in its fourth section. I would suggest you not spend time on Docker Swarm unless you have a compelling reason to do so.

## A Dozen Dockerfile Instructions

`FROM` specifies the base (parent) image.  

`LABEL` provides metadata. Good place to include maintainer info.  

`ENV` sets a persistent environment variable.  

`RUN` runs a command and creates an image layer. Used to install packages into containers.  

`COPY` copies files and directories to the container.  

`ADD` copies files and directories to the container. Can upack local .tar files.  

`CMD` provides a command and arguments for an executing 
container. Parameters can be overridden. There can be only one CMD.  

`WORKDIR` sets the working directory for the instructions that follow.  

`ARG` defines a variable to pass to Docker at build-time.  

`ENTRYPOINT` provides command and arguments for an executing container. Arguments persist.  

`EXPOSE` exposes a port.  

`VOLUME` creates a directory mount point to access and store persistent data.

## Docker Commands

**Images**

[----------]

**Containers**

[----------]

**Networking**

[----------]
