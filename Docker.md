## Docker

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

`docker build -t [image-name]:1.0`

`docker image ls`

`docker image rm [image-name]:3.5`

`docker pull [image-name]:1.0`

`docker push [repo-name]/[image-name]:2.0 `

**Containers**

Run a container in interactive mode

`docker run -it ubuntu bash`

List all containers

`docker ps -a`

Stop a container

`docker stop [container-name|container-id]`

Remove a container

`docker rm [container-name|container-id]`

Execute a new process in an existing container

`docker exec -it [container-name] bash`

Inspect a container

`docker inspect [container-name]`

`docker logs [container-name] --since 10m`

`docker logs -f [container-name]`

Expose port

`docker run -p [host-machine-port]:[container-port] ubuntu bash`

Set environment variables

`docker run -e MYVAR1 --env MYVAR2=foo --env-file ./env.list ubuntu bash`

Mount Volume

`docker run -v [directory-path-in-host-machine]:[directory-path-in-container] ubuntu bash`

## Scaling Docker

The following concepts relate to using docker effectively.

**Process has PID 1 inside docker container**

The [`--init`  flag](https://docs.docker.com/engine/reference/run/#specify-an-init-process) of `docker run` causes the `tini` init system to be used as the `ENTRYPOINT`. As a consequence, the application running in the container will be a child process of the init system so that it can take care of signal handling and zombie reaping

**The PID 1 problem: reaping zombies**

Unix processes are ordered in a tree. Each process can spawn child processes, and each process has a parent except for the top-most process.

This top-most process is the init process. It is started by the kernel when you boot your system. This init process is responsible for starting the rest of the system, such as starting the SSH daemon, starting the Docker daemon, starting Apache/Nginx etc. Each of them may in turn spawn further child processes.

![Docker-1]()

Nothing special so far. But consider what happens if a process terminates. Let's say that the bash (PID 5) process terminates. It turns into a so-called "defunct process", also known as a "zombie process".

![Docker-2]()

Why does this happen? It's because Unix is designed in such a way that parent processes must explicitly "wait" for child process termination, in order to collect its exit status. The zombie process exists until the parent process has performed this action, using the [waitpid()](http://linux.die.net/man/2/waitpid) family of system calls.

Most of the time this is not a problem. The action of calling `waitpid()` on a child process in order to eliminate its zombie, is called "reaping". Many applications reap their child processes correctly. In the above example with sshd, if bash terminates then the operating system will send a SIGCHLD signal to sshd to wake it up. Sshd notices this and reaps the child process.

![Docker-3]()

But there is a special case. Suppose the parent process terminates, either intentionally (because the program logic has determined that it should exit), or caused by a user action (e.g. the user killed the process). What happens then to its children? They no longer have a parent process, so they become "orphaned" (this is the actual technical term).

And this is where the init process kicks in. The init process -- PID 1 -- has a special task. Its task is to "adopt" orphaned child processes (again, this is the actual technical term). This means that the init process becomes the parent of such processes, even though those processes were never created directly by the init process.

![Docker-4]()

**Why zombie processes are harmful**

A child that terminates, but has not been waited for becomes a "zombie". The kernel maintains a minimal set of information about the zombie process (PID, termination status, resource usage information) in order to allow the parent to later perform a wait to obtain information about the child. As long as a zombie is not removed from the system via a wait, it will consume a slot in the kernel process table, and if this table fills, it will not be possible to create further processes.

**Relationship with Docker**

Let's look at a concrete example. Suppose that your container contains a web server that runs a CGI script that's written in bash. The CGI script calls grep. Then the web server decides that the CGI script is taking too long and kills the script, but grep is not affected and keeps running. When grep finishes, it becomes a zombie and is adopted by the PID 1 (the web server). The web server doesn't know about grep, so it doesn't reap it, and the grep zombie stays in the system.
