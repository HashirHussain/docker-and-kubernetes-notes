# Docker & Kubernetes(K8s) notes
## Table of contents

- What is Docker
- What are Containers
- What are Images in Docker
- What are Virtual Machines (VMs)
- What is Hypervisor
- Containers Vs Virtual Machines
- What is Docker Hub

## What is Docker
Docker is an open source PaaS platform for building, deploying and managing software in package called containers.

## What are containers
Containers are portable unit of software in which application code is packaged along with it's dependencies. in Docker, containers are running instance of an Image.

## What are Images in Docker
Docker image is a file that contains layer by layer set of instructions to run an application. Docker Image contains application code, libraries, tools, dependencies and other files needed to make an application run. In fact containers are running instance of an Image. `docker build` command use to create an Image.

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

| Containers      | Virtual Machines |
| ----------- | ----------- |
| OS level isolation   | Hardware level isolation         |
| lightweight (KBs / MBs)   | Heavyweight (GBs)        |
| Boots in seconds      | Takes few minutes to boot       |
| destroyed and re-created rather than moving   | Can move from one host to another        |
| Consumes less resources   | Consumes large amout of resources        |

## What is Docker Hub
[Docker Hub](https://hub.docker.com/) is the online registry tool for Docker. You can use, publish and share Docker Images via Docker Hub.
