# AKS (Azure Kubernetes Service)

## Overview

In this lesson, we will discuss **Azure Kubernetes Service (AKS)**, a managed service that makes deploying, managing, and scaling containerized applications using Kubernetes in the cloud so much easier. AKS makes it easy so that the majority of Kubernetes cluster management is managed automatically, which allows the developers to concentrate on writing the code and deploying the application.

## Lesson Outcomes

By the end of this lesson, you will be able to:

1. Understand the idea of cloud computing and its advantages.
2. Know the main key features and benefits of Azure Kubernetes Service (AKS).
3. Understand what AKS is good for and its benefits in managing containerized applications.
4. Familiarize with AKS and how its cloud services capabilities are simplified and how it is integrated with Azure households infrastructure management.
5. Be aware of the main advantages of AKS, such as managed control planes, node pools, and auto-scaling.

## Explanation

### What is Cloud Computing?

Cloud computing is a system that allows companies to use internet-based resources to rent the facilities such as servers, storage, and databases. Therefore there is no need for organizations to invest and maintain physical hardware anymore.

- **Benefits**: 
  - **Cost Efficiency**: You pay just for how much you consume.
  - **Scalability**: Grow your resources according to your necessity without investing in advance.
  - **Flexibility**: Use cloud services from anywhere you want.
 
### What is Azure?

Azure is the name for Microsoft’s cloud-services platform providing a suite of computing, storage, networking, and analytics services. Azure is a platform that allows organizations to build, run and manage applications without having to manage the underlying infrastructure themselves.

### What is Kubernetes?

Kubernetes is an open-source platform designed to automate the deployment, scaling, and operation of application programs that have been containerized. Kubernetes ensures that the applications are deployed in a stable manner and are highly efficient in scaling across clusters of machines.

### What is Azure Kubernetes Service (AKS)?

Azure Kubernetes Service (AKS) is a large Azure service provided by Microsoft that has the option of Managed Kubernetes. Developers are no longer the writers of infrastructure, Kubernetes has been abstracted away for such that applications are required to be maintained as this is done for them.

- **Why Use AKS?**
  - **Managed Kubernetes**: Azure handles the complexity of maintaining the Kubernetes control plane.
  - **Scalable and Flexible**: Easily scale your applications up or down based on demand.
  - **Integrated Security**: Built-in security features, including Role-Based Access Control (RBAC) and Azure Active Directory (AAD) integration.
  - **Cost-Effective**: You only pay for the virtual machines in the cluster. The Kubernetes control plane is free.
  
### Key Features of AKS

1. **Managed Control Plane**: Azure manages the Kubernetes master nodes, freeing developers from maintaining the control plane.
2. **Node Pools**: Different workloads can run on different types of virtual machines.
3. **Auto-Scaling**: AKS automatically adjusts the number of nodes based on the workload demand.
4. **Developer Tools Integration**: Seamless integration with Azure DevOps, CI/CD pipelines, and other Azure services like Azure Monitor.
5. **Monitoring & Logging**: Integrates with Azure Monitor for cluster health and performance tracking.

### Why Use AKS for Kubernetes?

- **Reduced Complexity**: AKS manages the Kubernetes infrastructure, allowing developers to focus on building applications.
- **Tightly Integrated with Azure**: Works seamlessly with Azure services like Azure Monitor, Azure Active Directory, and Azure DevOps.
- **High Availability**: AKS offers built-in high availability with automatic scaling and load balancing.
- **Cost Efficiency**: Only pay for the virtual machines used for the worker nodes, with no charge for the control plane.

## Suggested Reading

1. [Azure Kubernetes Service Overview](https://azure.microsoft.com/en-us/services/kubernetes-service/)
2. [Kubernetes Official Documentation](https://kubernetes.io/docs/)
3. [Azure and Kubernetes: A Winning Combination](https://learn.microsoft.com/en-us/azure/aks/intro-kubernetes)

