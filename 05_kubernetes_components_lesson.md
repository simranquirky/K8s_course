# **Kubernetes Components – A Quick Introduction**

## **Overview**

In this lesson, we will dive deeper into the **key Kubernetes components** that we introduced in the previous lesson. Understanding these components will help you manage and operate a Kubernetes cluster effectively by seeing how they interact and function together to run containerized applications.

## **Lesson Outcomes**

By the end of this lesson, you will:

- Understand the role and function of the **control plane** and **worker node** components.
- Learn about the key components such as **API Server**, **Scheduler**, **Kubelet**, and **etcd**.
- Get a better idea of how each component interacts to ensure smooth operation within a Kubernetes cluster.

## Explanation

## **Core Components of Kubernetes**

Comprehending Kubernetes, Bit by Bit
Let's examine each of the components in more detail now that we are aware of their high-level inclusions in Kubernetes.

### The API Server
As the name suggests, Kubernetes's API server, kube-apiserver, is in charge of hosting the APIs that control the remainder of the cluster and enable administrators to communicate with it. Kube-api-server serves as the framework for all other Kubernetes applications.

The master node or nodes within your cluster, if you have multiple master nodes, host the API server.

- **Role**: The API server acts as the central management point for the cluster. All communication with the Kubernetes cluster happens via the API server, making it an essential component for managing resources.
- **How it works**: The API server serves the Kubernetes API, through which you can create, update, or delete resources like pods, services, and deployments.

### Kube Scheduler

Kubernetes' ability to autonomously determine how to divide workloads among a cluster of computers is its primary selling point. These choices are made by the software program known as the scheduler, or kube-scheduler.

Kube-scheduler continuously checks the status of pods running in Kubernetes and determines which nodes should host them (unless administrators have designated a node with a DaemonSet or similar setup). In order to prevent workload interference and guarantee that only healthy nodes host workloads, the scheduler aims to distribute loads equally throughout the cluster.

- **Role**: The scheduler decides where to run newly created pods that don't have an assigned node. It checks available resources and schedules pods accordingly.
- **How it works**: It looks at things like resource requirements, affinity/anti-affinity rules, and other constraints to determine which node is best suited for each pod.

### Kube Controller Manager
The Kubernetes controller—also known as kube-controller-manager—is a collection of controllers. They take care of things like node monitoring and service and pod endpoint management.

- **Role**: This component runs controllers that are responsible for making sure the desired state of the cluster is maintained. These controllers run continuously to monitor and correct the state of resources.
- **How it works**: For example, the **ReplicaSet Controller** ensures that the correct number of pods are running based on the deployment configuration.

###  etcd

Etcd, a built-in key-value store offered by Kubernetes, houses the information needed to administer clusters.

In addition, data related to Kubernetes-based apps is not stored by Etcd. Applications must have their own storage for any data they generate, log, or otherwise produce. Usually, a storage volume of some sort is used for this. Etcd, which is exclusively in charge of hosting the data needed to monitor cluster status, control access requests, and other tasks, is separate from storage volumes.

- **Role**: A key-value store that contains the configuration and state of the Kubernetes cluster. It is used to store all information about the cluster, including the state of nodes, pods, deployments, and more.
- **How it works**: All changes made through the API server are stored in **etcd**. It provides a reliable and consistent way to store critical cluster data.

### Kubernetes Pods

Workloads are hosted by Kubernetes pods. YAML files are used to define pods. These files specify which container or containers each pod should use, along with optional configuration information such as commands to run or networking ports to expose.

In Kubernetes, pods serve as the primary building pieces for workloads. Pods are used to host any apps you wish to run in Kubernetes. So are any tools you would require to assist you manage your apps, including logging agents.

We will learn more about pods in upcoming lessons

### Kubernetes Nodes
In Kubernetes, nodes are the primary infrastructural building components. Both the Kubernetes control plane software and pods are hosted on these actual or virtual machines.

Master and worker nodes are the two different kinds of nodes as mentioned earlier. An operating system based on Linux must be installed on master nodes. Windows or Linux can be installed on worker nodes.

It's crucial to realize that Kubernetes does not control the nodes themselves, even if it is in charge of monitoring which nodes in a cluster are available. Users are responsible for maintaining and safeguarding the operating system, file system, and (if your nodes are virtual machines) the hypervisor.

To use the famous “pets vs. cattle” analogy, Kubernetes just sees nodes as “cattle” that can be joined to a cluster and used to host resources, not “pets” that it needs to treat specially and manage. Kubernetes doesn’t really care what is happening inside a node as long as the node is ready and able to host workloads.

### **Kubelet**

Each node is controlled by an agent known as Kubelet. Every node has a Kubelet instance that allows Kubernetes to monitor its state. Furthermore, Kube-proxy, a network proxy that runs on each node, controls network settings for pods that are housed on nodes.

- **Role**: The **Kubelet** is an agent that runs on each worker node. It ensures that the containers within pods are running in the desired state.
- **How it works**: It communicates with the **API Server** and receives instructions about the pods that should be running on the node, checking their status, and making adjustments if needed.

### Kubernetes DNS Server

A DNS server that understands the internal status of your cluster and can resolve DNS names appropriately is required for the majority of Kubernetes settings. Kubernetes offers Cluster DNS, its own DNS server, to make this simple.

Alternative DNS servers are offered by certain Kubernetes distributions, particularly those made to operate in the cloud. This can assist in balancing internal networking for Kubernetes with network configurations in cloud-based environments.

### Kubernetes Dashboard

An integrated web-based dashboard is provided by Kubernetes. The dashboard is helpful for basic cluster monitoring and management, but it cannot handle all administrative duties; for some, you will need to utilize the Kubernetes CLI tool, kubectl.

![dashboard](https://upcloud.com/media/kubernetes-dashboard.png)
Source:https://upcloud.com/media/kubernetes-dashboard.png


Alternative or personalized dashboards are available in certain Kubernetes distributions, such as OpenShift.
### **Container Runtime**

- **Role**: The container runtime is responsible for pulling images and running containers on the nodes.
- **How it works**: Kubernetes doesn’t dictate which runtime to use, but **Docker** and **containerd** are popular choices. The container runtime is what Kubernetes uses to run containers based on the specifications provided by the Kubelet.

### **Kube Proxy**

- **Role**: The **Kube Proxy** ensures that network traffic is properly routed between services and pods within the cluster.
- **How it works**: It maintains network rules on the nodes to enable communication between pods and external clients. It helps with load balancing, ensuring that traffic is routed correctly.

## Suggested Reading
- [Kubernetes Components Documentation](https://kubernetes.io/docs/concepts/overview/components/)