# DevOps

## Table of Content

- [What is DevOps](#what-is-devops)
    - [DevOps Cycle](#devops-cycle)
    - [Why do we need DevOps](#why-do-we-need-devops)
- [Virtualization](#virtualization)
    - [Interest of Virtualization](#interest-of-virtualization)
- [Cotainers](#containers)

## What is DevOps

`devOps` is a combination of cultural philosophies, practices and tools that increases an organization’s ability to deliver applications and services at high velocity.

FR definition: pratique technique visant à l'unification du développement logiciel et l'administration des infrastructures informatiques notamment l'administration système.

### DevOps Cycle

![devops-cycle](/devOps/devOps/resources/devops-cycle.png)

This is the lifecycle of a product iteration from `development` to `production`.

Dev Part:

- `plan`
- `code`
- `build`
- `test`

Ops Part:

- `release`
- `deploy`
- `operate`
- `monitor`

### Why do we need DevOps

=> to insure `portability of applications` and to avoid the typical problem of "It works on my machine".

=> to insure that we *consider the deployment environment from scratch*.

## Virtualization

`operating system`: system software that manages computer hardware and software resources, and provides common services for computer programs 

FR definition: ensemble de programmes qui dirige l'utilisation des ressources d'un ordinateur par les logiciels applicatifs

`virtualization`: process of creating a simulated, or virtual, computing environment as opposed to a physical environment.

FR definition : exécution d'environnement isolé sur une machine hôte. Elle permet l'abstraction des ressources matérielles. 

Virtualization is used to *isolate* an environment. We can virtualize:
- `operating systems` (system virtualization = *Virtual Machine*) 
- `applications` (application virtualization = *Virtual Environment*)

`hypervisor`: software that executes *Virtual Machines*.

FR definition : plateforme de virtualisation système. Il permet l'exécution de plusieurs OS sur la même machine.

![hypervisor-img](/devOps/devOps/resources/img-hypervisor.png)

### Interest of Virtualization

- A server that uses `15%` of its resources has almost the same need of electricity than a server that uses `95%` of its resources.

- It reduces the number of server required to run several applications.

## Containers

This refers to a native functionality of the Linux kernel. A container is a `Virtual Environment`. It is not a `Virtual Machine`. What is the difference?

![containers-vs-vms](/devOps/devOps/resources/containers-vs-virtual-machines.jpg)

Containers do not need to **have their own OS**. They rely on only what they strictly need through the Container Engine. This is a humongous save in resources.

- Virtual Machines relie on `baremetal` (there is only the hypervisor directly on the hardware part).

### Interest of Containers

- isolated environments
- light
- portable
- highly scalable
- ideal for microservices architectures
