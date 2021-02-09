# Azure

## Introduction
### What is Azure?  

Azure is Microsoft's cloud computing platform.  Azure supports IaaS, PaaS, and SaaS.  Services such as VMs, website and database hosting, and AI/Machine Learning.

### What is cloud computing?

Cloud computing is similar to shopping at a store, where you get to pick what products you want.  Instead of regular products found in a store, you are able to buy more powerful cloud-based machines (think better CPU, increased storage, more RAM, etc.).  Computational power can be added/removed as needed, which saves initial investment cost considerably.  Cloud providers also maintain the systems in the background, such as updates, creating backups, and sustain perpetual uptime.  

Paying for only what you need has many benefits, including:

* Lower operating costs  

* Run infrastructure more effeciently  

* Scale hardware as needed

Simply put, cloud computing allows people to "rent" compute power and storage from a providers datacenter, to be used as needed.  

**Main cloud computing benefits**:  

* **Reliability**: Depending on the service agreement with the provider, cloude-based services often provide continuous user experience with no apparent downtime, even when things go wrong.

* **Scalability**: Applications in the cloud can be scaled in two different ways:  

    * *Vertically*: Computing capacity increased by adding additional RAM or CPUs.

    * *Horizontally*: Computing capacity can be increaded by adding instances of a resource, such as additional VMs.

* **Elasticity**: Cloud-based applications can be configured to always have the resources needed.

* **Agility**: Offers the ability to deploy/reconfigure quickly when requirements change.

* **Geo-distribution**: Regional datacenters are usually offered, allowing deployment around the globe, ensuring customers have best performance available.  

* **Disaster recover**: Backup services, data replication, and geo-distribution means that your data will be safe in the event of a disaster.  

### Cloud Service Models

Cloud computing falls into one of the following computing models:  

| Computing Model                        | Description                                                                                                                                                                                                                                   |
|----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| IaaS (**Infrastructure as a Service**) | This is the closest computing model to managing physical servers.  Operating system and network configuration maintenance is left to the user.  One main advantage for IaaS is the rapid deployment of new devices.                           |
| PaaS (**Platform as a Service**)       | This computing model is a managed hosting environment.  The cloud provider manages the VMs and networking resources, allowing users to deploy applications into the managed hosting environment.                                              |
| SaaS (**Software as a Service**)       | This computing model is completely managed by the cloud provider, including all aspects of the application environment, VMs, networking resources, data storage, and applications.  Only data is needed from the user to run the application. |

The following image highlights the level of responsibility for the cloud providers and users, based on computing model:

![!Shared Responsibilities](https://nicklyss.com/media/uploads/2021/02/shared-responsibility.png)

### What is serverless computing?

Overlapping with PaaS, serverless computing allows developers to build applications faster by eliminating the need for them to manage infrastructure.  Through serverless computing, the cloud provider automatically provisions, scales, and manages the infrastructure required.  Serverless architectures are extremely scalable and event-driven and only use resources when the are requested.  

