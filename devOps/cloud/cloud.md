# Cloud Computing

## Table of Contents

- [What is the Cloud?](#what-is-the-cloud)
- [Type of Services](#type-of-services)
    - [IaaS](#iaas)
- [OIV](#oiv)
- [Everything fails all the time](#everything-fails-all-the-time)

## What is the Cloud?

## Type of Services

There are different types of services available. Depending on the type of service provided, some layers will be supported by **the cloud provider** and some layers will be let at **the charge of the client**.

- **IaaS** (Infrastructure as a Service): 
- **CaaS** (Cloud as a Service):
- **PaaS** (Platform as a Service):
- **FaaS** (Functions as a Service):

![img_1](/devOps/cloud/resources/type-services.png)

Here is a quick overview of what is managed by who:

![img_2](/devOps/cloud/resources/cloud-computing.jpg)

### IaaS

The **Infrastructure as a Service** model provides compute, memory, storage, networking and related software, such as operating systems and databases. It is very flexible and useful for hosting custom-built applications.

The advantages of IaaS are the following:

- **Pay for What You Use**: Fees are based on usage metrics
- **Dynamically Scale**: Rapidly add capacity in peak times and scale down as needed

![img_3](/devOps/cloud/resources/iaas.png)

### PaaS

![img_4](/devOps/cloud/resources/paas.png)

### SaaS

![img_5](/devOps/cloud/resources/saas.png)

## OIV

The french digital institutions have special classifications they call ***Opérateurs d'Importance Vitale*** (Critical Operators). These cloud services are critical because without them, the ability of the nation to survive.

It includes different sectors such as economy, financial, technology, health...

![img_6](/devOps/cloud/resources/oiv-par-secteur.jpg)

## Everything fails all the time

The CTO of AWS, Wegner Vogels, once said `everythin fails, all the time` so the service has to keep running even if its VMs are down.

*Netflix* developed a toolbox called ***Simian Army*** which aims at testing the ability of the service to keep running even if its VMs are down.
It is composed of 8 tools:

![img_7](/devOps/cloud/resources/simian-army.png)