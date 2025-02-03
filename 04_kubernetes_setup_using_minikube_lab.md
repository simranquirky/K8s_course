# **Kubernetes Setup Using Minikube**

## **Lab Overview**

In this lab, you will set up a local Kubernetes cluster using **Minikube**. Minikube is a tool that allows you to run Kubernetes clusters on your local machine, simulating a Kubernetes environment for development and testing. By the end of this lab, you’ll have a running Kubernetes cluster and be able to view its architecture.

## **Pre-requisites**

Before starting this lab, ensure you have:

- A computer with at least **2GB of RAM** and **20GB of free disk space**.
- **Virtualization software** such as VirtualBox, HyperKit, or Hyper-V, depending on your OS.

## **Outcomes**

By the end of this lab, you will be able to:

1. Install and set up Minikube.
2. Start a local Kubernetes cluster using Minikube.
3. View the components of the Kubernetes architecture (Control Plane and Worker Nodes).
4. Check the status of your local cluster and its resources.

## **Description**

This lab will guide you through the process of setting up a local Kubernetes cluster using Minikube. You’ll start Minikube, explore its architecture, and understand the key components that make up a Kubernetes cluster. This will help you get hands-on experience with Kubernetes in a local environment, without needing a cloud-based setup.

### **Why Use Minikube?**

Minikube is a lightweight Kubernetes implementation that creates a single-node Kubernetes cluster on your local machine. It’s an excellent tool for developers who want to:

- **Learn Kubernetes:** Minikube provides a playground to explore Kubernetes commands, concepts, and architecture.
- **Test Kubernetes Applications:** Before deploying applications to a production environment, you can use Minikube to ensure they work as expected.
- **Develop Locally:** Minikube allows you to develop and test applications locally, speeding up the development cycle.

## **TASKS**

### **Task 1: Install Minikube**

1. Install Minikube following the official guide for your operating system:
    
    Minikube installation is straightforward, and it varies slightly depending on your operating system. Let’s walk through the installation process for each platform.
    
    - **Installing Minikube on macOS:**
    
    The easiest way to install Minikube on macOS is using Homebrew:
    
    `brew install minikube`
    
    Homebrew will download and install Minikube along with any necessary dependencies.
    
    - **Installing Minikube on Linux:**
    
    For Linux, you can install Minikube using the following commands:
    
    ```sql
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
    
    sudo install minikube-linux-amd64 /usr/local/bin/minikube
    ```
    
    These commands download the Minikube binary and install it in your `/usr/local/bin` directory, making it accessible from anywhere in your terminal.
    
    **Installing Minikube on Windows:**
    
    Windows users can install Minikube by downloading the executable from the [Minikube releases page](https://github.com/kubernetes/minikube/releases).
    
    1. Download the latest minikube-installer.exe.
    2. Run the installer and follow the installation prompts.
    
    Alternatively, you can use choco (Chocolatey) to install Minikube:
    
    `choco install minikube`
    
2. Once installed, verify Minikube installation:
    
    ```bash
    minikube version
    ```
    
    You should see the Minikube version details in the output.
    

### **Task 2: Start the Kubernetes Cluster**

1. Start your local Kubernetes cluster with Minikube:
    
    ```bash
    minikube start
    ```
    
    Minikube will download the required Kubernetes images, set up a virtual machine, and start the cluster.
    
2. Wait for the process to complete. Once it’s done, you will have a local Kubernetes cluster running.

### **Task 3: View Cluster Architecture**

After the cluster is started, Minikube provides a way to visualize the architecture of your Kubernetes setup.

1. **View the Control Plane and Worker Nodes**:
    - Minikube will automatically set up a **Control Plane** (Master node) and **Worker Nodes**. To see the status of your cluster:
        
        ```bash
        minikube status
        ```
        
    
    This command will show the state of your cluster and indicate whether it’s running, paused, or stopped.
    
2. **Check Kubernetes Components**:
You can view the status of Kubernetes components in your cluster with the following command:
    
    ```bash
    kubectl get nodes
    ```
    
    This will show you the nodes in the cluster (both Control Plane and Worker Nodes).
    
    Note: `kubectl` is the Kubernetes command-line tool for managing clusters. Minikube includes `kubectl.`
    
3. **Access the Kubernetes Dashboard**:
Minikube provides a Kubernetes Dashboard for visualizing the cluster architecture:
    
    ```bash
    minikube dashboard
    ```
    
    This will open a web-based Kubernetes Dashboard in your default browser, where you can explore the architecture in more detail, such as the nodes, pods, services, and deployments.
    

### **Task 4: Verify the Cluster Architecture**

1. In the **Minikube Dashboard**, move to the Cluster's page:
    - In the Nodes section you will see minikube listed, click on minikube to get all the pods running inside the cluster.
    - You will notice it includes components like the API server, scheduler, and controller manager.
    - **Worker Nodes**: These nodes run your application workloads (pods). Cuurrently if you go to pod section under workload you won't find anything as we don't have any workload appliaction running.
    - **Pods**: The smallest deployable units in Kubernetes that run your containerized applications.
3. You can also run the following command to view all running resources (nodes, pods, etc.):
    
    ```bash
    kubectl get all --all-namespaces
    ```
    

Note: You will learn about Kubeclt commands in detail in the upcoming lessons.

## **Submission Guidelines**

- Submit a screenshot of the `minikube status` output showing your cluster status.
- Submit a screenshot of the **Minikube Dashboard** showing the minikube cluster details.
- Provide a screenshot of the `kubectl get nodes` output showing the nodes.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/start/)