## **Kubernetes Architecture**

## **Overview**

In this lesson, you will know about the architecture of **Kubernetes**. Understanding Kubernetes architecture is crucial because it helps you see how Kubernetes components work together to deploy, manage, and scale containerized applications efficiently.

## **Lesson Outcomes**

By the end of this lesson, you will:

- Understand the **core components** of Kubernetes.
- Learn how Kubernetes uses a **control plane** to manage the cluster.
- Understand the role of **nodes**, **pods**, and **services** in Kubernetes architecture.
- Know how to visualize the flow of tasks in Kubernetes from the control plane to the worker nodes.

## Explanation

Before we dive into Kubernetes architecture, it’s important to understand what a **cluster** is and why it’s crucial for container orchestration.

### **What is a Cluster?**
A cluster is a set of computers (usually called nodes) that work together to execute applications, share resources, and provide the availability and scalability services. A Kubernetes cluster is in fact the set of nodes that work together: for deploying, managing a containerized application.
 
Nodes are the individual machines (physical or virtual) in the cluster.
Clusters are typically managed by orchestration tools like Docker Swarm and Kubernetes.

Why Do We Need Clusters?

Deploying containers in a distributed system at scale: you can't always trust 1 machine per app to do everything. There are the benefits of clusters as below:

- Scalable: Placing of container may be on various machines so that your app can scale up and take hits.
- High Availability: when a node fails, the load is redistributed to other nodes so services are still alive.
- Resource management: Clusters can manage the resources (CPU, memory …) on all the nodes efficiently

In Simple Terms:
- With no cluster: you can only run containers on one machine, which means no scaling and can eventually break.
- With cluster: Scaling is easy. To horizontally scale containers -- distribute them across many machines, and provide load balancing and fault tolerance. 

### **Master-Slave Architecture: The Foundation of Kubernetes**

Before we get into Kubernetes specifics, it helps to understand the basic **master-slave architecture**, which is commonly used in distributed systems, including Kubernetes.

**Master-Slave Architecture**

- **Master Node**: The central control point for the cluster. It manages and controls the overall cluster state, making decisions like scheduling and scaling.
- **Worker Nodes (Slave Nodes)**: These nodes run the containerized applications (pods) that are scheduled by the master.

In Kubernetes:

- The **master node** (also known as Control plane) is responsible for managing the state of the cluster.
- The **worker nodes** are responsible for running the containers.

## **Key Components of Kubernetes Architecture**

![image.png](https://techdozo.dev/wp-content/uploads/2021/07/K8-Architecture.png.webp)
Source : https://techdozo.dev/wp-content/uploads/2021/07/K8-Architecture.png.webp 

### **Control Plane**

The **control plane** is the part of Kubernetes responsible for making global decisions about the cluster (like scheduling pods) and responding to cluster events (such as starting up a new pod when a deployment's replica count isn't satisfied).

- The **control plane** components can run on any machine within the cluster. However, setup scripts typically start all control plane components on a single machine, separate from user containers.

**Control Plane Components**:

- **Kube API Server**
- **Scheduler**
- **Controller Manager**
- **etcd**

### **Kube API Server**

The **API Server** is the front end of the control plane, exposing the Kubernetes API. It's responsible for handling requests and making changes to the cluster state.

- It is horizontally scalable, meaning you can run multiple instances and balance traffic between them.

Example: When you run commands to deploy, manage, or update applications, these requests are routed through the API server.

### **etcd**

**etcd** is a distributed key-value store used by Kubernetes to store all cluster data, including the desired state and configuration.

- It's highly available and consistent, but you need a backup plan in case of failure, as it's critical to cluster operation.

### **Kube Scheduler**

The **Scheduler** is responsible for watching for newly created pods without an assigned node and choosing the best worker node to run them on.

**Factors Considered**:

- Resource requirements
- Hardware/software constraints
- Affinity and anti-affinity rules
- Data locality and inter-workload interference

### **Kube Controller Manager**

The **Controller Manager** runs controllers that handle routine tasks in the cluster, ensuring the desired state is maintained.

- **Node Controller**: Handles node failures.
- **Job Controller**: Manages one-off jobs.
- **ServiceAccount Controller**: Manages service accounts for new namespaces.

### **Worker Nodes**

**Worker nodes** run the applications (pods). These nodes can be either **Linux** or **Windows** based, and Kubernetes allows a mix of both types in a single cluster.

**Worker nodes run three essential services**:

1. **Kubelet**
2. **Container Runtime**
3. **Kube Proxy**

### **Kubelet**

The **Kubelet** is the main agent on each worker node that ensures containers are running as expected.

- It watches for new work tasks from the API server and reports the status of the containers back to the master.

### **Container Runtime**

The **Container Runtime** is responsible for running containers on each node.

- Kubernetes used to use **Docker**, but since 2016, it supports other runtimes through the **Container Runtime Interface (CRI)**, like **containerd** (the default container runtime in most environments).

### **Kube Proxy**

**Kube Proxy** is responsible for managing network communication between services and pods within the cluster.

- It maintains network rules on nodes that enable internal and external communication to your pods.

### **Putting It All Together**

Here’s how the components work together:

1. **You create a pod**: You define a pod that includes the containers you want to run.
2. **Kubernetes schedules the pod**: The **Scheduler** decides where to run the pod based on available resources on worker nodes.
3. **The pod is deployed on a worker node**: The **Kubelet** ensures that the pod runs properly.
4. **Service exposes the pod**: If external access is required, a **Service** exposes the pod.

### Summary:

- **Control Plane**: The brain of the Kubernetes cluster, managing state and making global decisions.
- **Master Node**: The machine running control plane components.
- **Worker Nodes**: Machines that run the applications (pods) and communicate with the control plane.
- **Pods**: The smallest deployable unit containing containers.
- **Services**: Expose pods to the outside world or within the cluster.

## Suggested Reading
- [Kubernetes Architecture Documentation](https://kubernetes.io/docs/concepts/architecture/)
