# Orchestration tools: Docker swarm and Kubernetes

## Overview

This lesson covers Docker Swarm and Kubernetes, both highly popular container orchestration tools. We'll start with Docker Swarm, its weaknesses, and what it's missing, then proceed to Kubernetes, which bridges those gaps and has additional capabilities to deal with containerized applications at scale.

## Lesson Outcomes

By the end of this lesson, you will:

- Find out about Docker Swarm and its constraints.
- Learn why Kubernetes is a popular substitute and what advantages it offers.
- Compare Docker Swarm and Kubernetes to help you decide which tool to use based on your project requirements.

## Explanation

Let's begin by discussing the issues you learned in Lesson 1:

### **Recap of the Problem**

Handling multiple containers manually does not scale, particularly when you have large systems. You require automation for deployment, scaling, recovery, and so on.

This is where container orchestration tools such as Docker Swarm and Kubernetes step in.

### Docker Swarm

Docker provides **Docker Swarm** as its native orchestration tool. If you're already using Docker, Docker Swarm allows you to turn your Docker engines into a cluster that can handle deployment, scaling, and management of containers across multiple nodes.

### **Docker Swarm Features:**

- **Cluster Management**: Docker Swarm allows you to run several Docker engines as a single cluster.
- **Scaling**: You can scale services up or down with easy commands.
- **Load Balancing**: Dynamically distributes traffic between containers.
- **Easy Installation**: It is simple to install and is suitable for small projects.

### **Limitations of Docker Swarm:**

Although Docker Swarm is easy and works seamlessly with Docker, it lacks capabilities when dealing with intricate systems at scale.

- **Limited Auto-Scaling**: Docker Swarm does not have sophisticated auto-scaling capabilities. It can scale services manually or with limited automation.
- **Essential Networking**: Docker Swarm offers fundamental networking, and that may be lacking for high-complexity applications with various microservices.
- **Limited Ecosystem and Community Support**: The Docker Swarm ecosystem is smaller than that of Kubernetes. That translates into fewer tools, integrations, and community support.
- **Not Good for Production at Scale**: Docker Swarm might be hard to use when it comes to large, distributed and complex applications. 

Listing down the limitations straightforward may not make a lot of sense. You can understand them better by the following scenarios:

#### **Scenario 1: Scaling Based on Traffic Demand**

Let's think about running a shopping cart for an e-commerce platform. As the day progresses users browse through and add items to their cart, traffic increases throughout the day and reduces at night as people go to sleep.

**Challenge in Docker Swarm**:

- Docker Swarm allows you to scale services manually by increasing the number of replicas. But **auto-scaling** based on traffic demand (e.g., CPU utilization or request rate) is **not built-in**. You would need to use external tools or custom scripts for this, which is inconvenient and often unreliable.

**Limitation**: **No native auto-scaling** based on real-time traffic or system resource usage.

#### **Scenario 2: Networking Between Services**

Now, assume we are dealing with a microservices architecture for a streaming platform (transcoding video, user management & payments are all done in different containers.)

**Challenge in Docker Swarm**:

- While Docker Swarm supports basic service discovery, managing complex **network policies** (e.g., restricting access between certain services) can be tricky. For instance, you might want to ensure that the **payment service** can communicate only with the **user service** but **not** with the **video transcoding service**.

Limitation: Limited networking; no advanced network policy or fine grained controls over inter-service communication.

#### **Scenario 3: High Availability and Fault Tolerance**

Picture a banking application of yours which needs 99.99% uptime so users can withdraw in any hour of the day. You have your application running on multiple containers in Docker Swarm cluster. 

**Challenge in Docker Swarm**:

- If a **node** (a physical or virtual machine) in your Docker Swarm cluster fails, Docker Swarm will try to restart the container on another node. However, Swarm doesn’t guarantee the **rapid recovery** of failed services, and the process of rescheduling containers may take longer during a failure. This could result in **downtime**, affecting users.

**Limitation**: **Slow failover** and **limited self-healing** capabilities.

#### **Scenario 4: Resource Management**

Let’s say your **video processing service** requires significant **CPU resources** for transcoding, while your **user notification service** is lightweight but needs more **memory**.

**Challenge in Docker Swarm**:

- Docker Swarm provides basic resource allocation options, but it doesn’t allow you to specify precise limits or **requests** for CPU and memory per container. This can lead to resource contention between containers running on the same node, causing performance issues.

**Limitation**: **Limited resource management** and no fine-grained control over CPU/memory allocation.

### Why Kubernetes Is Better for Complex Applications

From the examples above, it’s clear that Docker Swarm is simpler but lacks the **advanced features** needed for larger, more complex applications. Kubernetes was designed to address these shortcomings with features like:

- **Auto-scaling** based on demand
- **Advanced networking** with **Network Policies**
- **Faster recovery** and **self-healing**
- **Efficient resource management** with **requests** and **limits**

### Kubernetes — The Advanced Solution

Kubernetes in short is called K8s.It is Open Source container orchestration platform which helps to mitigate most hard Docker Swarm limitations.
It is intended for production-scale containerized application management and is built to handle large-scale applications.

#### Key Features of Kubernetes:
- Pods: In the case of Docker Swarm, services are used, whereas Kubernetes works with pods that may consist of multiple containers.
- Auto-Scaling: Kubernetes provides super scalable auto-scaling in no time with CPU, memory, or even custom metrics to spin up an application.
- Self-Healing: Kubernetes will automatically restart your containers or replace them, if a container or pod dies you are up and running in no time!
- Highlighted Networking: Kubernetes, for microservices, allows more advanced networking, like network policies service discovery, and ingress controllers.
- Resource Usage: Kubernetes is able to make the best usage of CPU, memory, and storage on your nodes.
- Extensive Ecosystem and Community Backing: Kubernetes has a giant ecosystem with piles of tools and integrations that are backed by a huge community. 


## Suggested Reading
- [Deploying apps in Docker Swarm](https://docs.docker.com/guides/swarm-deploy/)
- [The history of Kubernetes](https://www.ibm.com/think/topics/kubernetes-history)