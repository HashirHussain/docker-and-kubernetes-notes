# Docker & Kubernetes(K8s) notes
## Table of contents

- What is Docker
- What are containers
- What are Images in Docker
- What are Virtual Machines (VMs)
- What is Hypervisor
- Containers Vs Virtual Machines


## What is Docker
Docker is an open source PaaS platform for building, deploying and managing software in package called containers.

## What are containers
Containers are portable unit of software in which application code is packaged along with it's dependencies. in Docker, containers are running instance of an Image.

## What are Images in Docker
Docker image is a file that contains layer by layer set of instructions to run an application. Docker Image contains application code, libraries, tools, dependencies and other files needed to make an application run. In fact containers are running instance of an Image. `docker run` command use to create a container for a specific Image.

## What are Virtual Machines (VMs)
A Virtual Machine is a virtual environment that behaves like an actual computer with its own CPU, memory, network interface and storage created on a physical hardware system. A software called Hypervisor is responsible to create VMs.  

## What is Hypervisor
Hypervisor is a software layer above host operating system that creates and runs one or more VMs by sharing underlying hardware resources.


## Containers Vs Virtual Machines(VMs)



