+++
date = 2019-09-21T15:38:00Z
description = "Explanation of Docker engine and difference between docker and a virtual machine"
hero = "/uploads/default-hero.jpg"
title = "What is Docker?"
[author]
avatar = ""
name = "Nino Sirchia"
+++

Maybe you've heard about [**Docker**](https://www.docker.com/), but maybe you stil do not have much clear what docker is.
In this post we will explore such technology and will go through 3 reason why you should definitely consider to migrate toward a docker based release of your software.

But let's start from the beginning: the Docker page on Wikipedia says that

> Docker is a set of platform-as-a-service (PaaS) products that use OS-level virtualization to deliver software in packages called containers.

Here we have a couple of keypoints that worth to explore a little bit.

The first keypoint is that **Docker is about virtualization**. The key goal of Docker is to bundle software in a infrastructure independent packages.
This means that you can deploy exactly the same package of an application both on Windows systems and on Linux systems.

This happens because the software packages that Docker allows to build contain the entire software stack, from Operting System to the application itself.

You may think: _"Well, just like running my application in Virtualbox or similar"_. The answer is no.

The difference between Virtualbox and Docker is that Virtualbox (just like Parallels, VMWare and other virtualization systems) creates an entire virtual guest machine on top of the host system. Docker, on the other hand, create a set of small guest environments, called **containers**, that rely on the host kernel. The following diagram shows the difference among them.

![DockerArchitecture](/res/images/docker_1.png "Docker architecture")

A shown in the left-hand of the picture, a virtual machine create the entire stack, from the Kernel to the application; the management of the virtual machines in on an Hypervisor.
A docker container, on the other hand, do not virtualize the kernel but relies on the kernel of the Host OS.

This makes the container much more lightweight then a virtual machine implying also better performances of the applications.


The second keypoint is that **Docker is a set of products**, not just a single tool.

These products are:
* a **sofware**, named docker daemon, that you can install in your laptop and will enable you to actually work with all the other products.
* a **registry**, named _Docker Hub_, that is a repository of the Docker images  
* a **cloud platform**, named _Docker Cloud_, that is a platform that provide several interesting functionalities to developers
* a **toolkit**, composed by **Docker Compose** and **Docker Swarm** that make the software deployment with Docker easier.

All of them have both a community edition, that is totally free of charge and an enterprise edition that requires the payment of a fee of $750 up to $2000 per year. Let me say that, unless you have very specific needs, the Community Edition will be definitely more then enough!

The docker daemon is the main entry point to start working with Docker. It can be installed in a machine and allows to manage the running containers thanks, also, to the interaction with the registry and other possible toolkits installed in the same host machine. 

## Why should you use docker?
Let's focus now on the main benefits of Docker.

#### 1. Easy deployment
For sure one of the main benefits of Docker is that it allows to deploy and run complex application very easily. The **Docker Hub** has a plethora of ready to use application, released as **Docker Images** that can be deployed with just one command on the CLI of your computer.
Of course, even the deletion of an application is easy like the deployment.


#### 2. Security
The docker containers are **100% segregated** each other. So a container is totally isolated from others, unless you decide otherwise.
This means that even if the application deployed in a container has some backdoors or is cracked by malicious users, the flaw is related only to that container and do not affect the other ones.


#### 3. Continuous Integration and Delivery
Docker is the perfect last mile of whichever CI/CD pipeline. Tools like [**Jenkins**](https://jenkins.io/ "Jenkins")  and [**Travis**](https://travis-ci.org/ "Travis") natively support the docker image building of software.
The Docker daemon and orchestrators like [**Kubernetes**](https://kubernetes.io/ "Kubernetes") or [**Docker Swarm**](https://docs.docker.com/engine/swarm/ "Swarm") allow also the autodeploy of the images. In a nutshell, docker is the perfect tool to make you work smarter and faster.  
