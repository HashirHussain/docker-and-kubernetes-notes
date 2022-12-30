# Docker & Kubernetes(K8s) notes

## Table of contents

- What is Docker
- What are Containers
- What are Images in Docker
- What are Virtual Machines (VMs)
- What is Hypervisor
- Containers Vs Virtual Machines
- What is Docker Hub
- Create a simple containerized application
  - prepare `Dockerfile`
  - Build an Image
  - Start an app container from Image
  - Working on container

## What is Docker

Docker is an open source PaaS platform for building, deploying and managing software in package called containers.

## What are containers

Containers are portable unit of software in which application code is packaged along with it's dependencies. in Docker, containers are running instance of an Image.

## What are Images in Docker

Docker image is a file that contains layer by layer set of instructions to run an application. Docker Image contains application code, libraries, tools, dependencies and other files needed to make an application run. In fact containers are running instance of an Image. `docker build` command use to create an Image from specific `Dockerfile`. Images are read-only and hence modification to an image is not possible after build.

![Many Containers can be created from single Docker image](/images/one-image-multiple-containers.jpg "Many Containers can be created from single Docker image")

## What are Virtual Machines (VMs)

A Virtual Machine is a virtual environment that behaves like an actual computer with its own CPU, memory, network interface and storage created on a physical hardware system. A software called Hypervisor is responsible to create VMs.  
Learn more here [What is a virtual machine?](https://www.vmware.com/topics/glossary/content/virtual-machine.html)

## What is Hypervisor

Hypervisor is a software layer above host operating system that creates and runs one or more VMs by sharing underlying hardware resources.  
learn more here [What is a hypervisor?](https://www.vmware.com/topics/glossary/content/hypervisor.html)

## Containers Vs Virtual Machines(VMs)

![Containers Vs Virtual Machine](/images/virtual-machines-vs-containers.jpg "Containers Vs Virtual Machine")
Both Docker and Virtual Machines are complimentary tools intended to improve the utilization of IT resources.

Virtual Machines has enabled enterprises to combine several servers running different application onto a single physical server even if they run different operating systems. While the number of VMs that can exist on a single IT infrastructure is constrained by the amount of CPU and RAM that they consume.

Whereas Containers party responsible to reduce the amount of consumption of IT resources. Containers often shares single OS instance and dependent libraries hence more focused on application code.

| Containers                                  | Virtual Machines                   |
| ------------------------------------------- | ---------------------------------- |
| OS level isolation                          | Hardware level isolation           |
| lightweight (KBs / MBs)                     | Heavyweight (GBs)                  |
| Boots in seconds                            | Takes few minutes to boot          |
| destroyed and re-created rather than moving | Can move from one host to another  |
| Consumes less resources                     | Consumes large amount of resources |

## What is Docker Hub

[Docker Hub](https://hub.docker.com/) is the online registry tool for Docker. You can use, publish and share Docker Images via Docker Hub.

## Create a simple containerized application

Docker can build or create images based on the "instructions" we write in `Dockerfile`.

### prepare `Dockerfile`

Here is the format of `Dockerfile`.

```
# Comment
INSTRUCTION argument
```

**The instructions are not case-sensitive. However, convention is for them to be UPPERCASE to distinguish them from arguments more easily.**

I'll work on a [sample Node.js application](/sample-app) but you can create your own application to practice on.

Open a terminal and change the directory to sample-app

`cd /path/to/sample-app`

Create an empty file called `Dockerfile` (without any file extension) at root level of the project and paste the blow content.

```
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
CMD ["node", "server.js"]
EXPOSE 8080
```

Docker runs instructions one after another/layer by layer from top to bottom. let us understand each instruction:

**FROM**

**`Dockerfile` must begin with `FROM` instruction
that specify the base image for subsequent instructions. It pulls image either locally or from online docker registry. Here "node" is the image and "18-alpine" is the tag. No tag name means pull the latest tag from the image.**

```
Syntax: FROM <Image>:<Tag>
```

learn more here: [Docker Docs - FROM](https://docs.docker.com/engine/reference/builder/#from)

**WORKDIR**

`WORKDIR` is used to define the working directory of a Docker container at any given time. Frequently used instructions like `RUN`, `CMD`, `ADD`, `COPY`, or `ENTRYPOINT` will be executed in the directory specified in `WORKDIR`.

```
Syntax: WORKDIR /my-project-path-inside-container
```

learn more here: [Docker Docs - WORKDIR](https://docs.docker.com/engine/reference/builder/#workdir)

**COPY**

The `COPY` instruction copies the files and directories inside a Docker container from your local machine.

```
Syntax: COPY <source-path> <destination-path-inside-container>
Destination path is typically define in `WORKDIR`.

```

learn more here: [Docker Docs - COPY](https://docs.docker.com/engine/reference/builder/#copy)

**RUN**

The `RUN` instruction will execute any commands in a new layer on top of the current image and commit the results. The resulting committed image will be used for the next step in the Dockerfile.

```
Syntax:
RUN <command>
RUN ["executable", "param1", "param2"]

```

learn more here: [Docker Docs - RUN](https://docs.docker.com/engine/reference/builder/#run)

**CMD**

`CMD` instruction executes at the time of running a container. It is asked to have one `CMD` command, If the `Dockerfile` has multiple `CMDs`, it only applies the instructions from the last one.

```
Syntax:
CMD ["executable","param1","param2"] (exec form, this is the preferred form)
CMD ["param1","param2"] (as default parameters to ENTRYPOINT)
CMD command param1 param2 (shell form)

```

learn more here: [Docker Docs - CMD](https://docs.docker.com/engine/reference/builder/#cmd)

**EXPOSE**

The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. We can interact with a running Container via exposed port from outside the container.

```
Syntax: EXPOSE <PORT_NUMBER>
```

learn more here: [Docker Docs - EXPOSE](https://docs.docker.com/engine/reference/builder/#expose)

### Build an Image

Open a terminal and change to directory to sample-app `cd /path/to/sample-app` and run the below command to build container Image.

```
docker build -t first-image .
```

You will see the output somewhat like this:
![Docker build output](/images/docker-build-output.jpg "Docker build output")

The `docker build` command uses the `Dockerfile` to build a new container image. You might have noticed that Docker downloaded a lot of “layers”. This is because you instructed the builder that you wanted to start from the `node:18-alpine image. But, since you didn’t have that on your machine, Docker needed to download the image.

The `-t` flag tags your image. Think of this simply as a human-readable name for the final image. Since you named the image `first-image`, you can refer to that image when you run a container.

The `.` at the end of the docker build command tells Docker that it should look for the Dockerfile in the current directory.

### Start an app container from Image

Now that you have an image, you can run the application in a `container`. Start the container using and specify the name of the image you just created:

```
docker run -p 3000:8080 first-image
```

`-p` flag creates a mapping between container's port with your host port i.e. `-p <host_port>:<container_port>`

After few milliseconds, will see the output like this in your computer:

![Container run output](/images/container-run-output.jpg "Container run output")
