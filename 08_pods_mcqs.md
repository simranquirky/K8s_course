# MCQ: Pods


## **Overview**

This quiz assesses your understanding of Kubernetes Pods, their functionalities, and the overall Kubernetes architecture.

## **Learning Objectives**

By the end of this quiz, you should be able to:

- Understand the role and functionality of Kubernetes Pods.
- Identify the key components of Kubernetes architecture.

## Question 1

Why does Kubernetes use Pods instead of managing containers directly?  
- [ ] To reduce the number of containers in the cluster.  
- [x] To provide an abstraction layer that simplifies container orchestration.  
- [x] To allow containers in the same Pod to share networking and storage resources.  
- [ ] To enable Pods to run on multiple nodes simultaneously.  

## Question 2

What happens if a Pod fails in Kubernetes?  
- [ ] The containers inside the Pod restart automatically.  
- [x] Kubernetes may reschedule the Pod on a different node.  
- [ ] The Pod becomes long-lived to maintain the desired state.  
- [x] A new Pod may be created by higher-level controllers like Deployments.  

## Question 3

Which resources are shared by containers within the same Pod?  
- [x] Networking (IP address and port space).  
- [ ] Individual container configurations for CPU and memory.  
- [x] Storage volumes.  
- [ ] External node resources.  

## Question 4

What are Pods in Kubernetes typically used for?  
- [x] Running one or more tightly coupled containers.  
- [ ] Hosting all services in a cluster.  
- [ ] Ensuring that containers run on multiple nodes.  
- [x] Providing a logical host for application-specific workloads.  

## Question 5

Which statement about Pods is **incorrect**?  
- [x] Pods are designed to be long-lived and never replaced.  
- [ ] Pods can share volumes for storing configuration data.  
- [x] Containers in a Pod can communicate using localhost.  
- [ ] Pods are the smallest deployable unit in Kubernetes.  


## Question 6

Which component is the front end of the Kubernetes control plane and handles requests to the cluster?  
- [x] Kube API Server  
- [ ] Kube Scheduler  
- [ ] etcd  
- [ ] Kube Controller Manager  

---

## Question 7

What is the role of the Kube Scheduler in Kubernetes architecture?  
- [ ] Managing container runtime on nodes  
- [ ] Exposing pods to external traffic  
- [x] Assigning pods to suitable worker nodes  
- [ ] Storing cluster state information  

---

## Question 8

Why does Kubernetes use Pods instead of managing containers directly?  
- [ ] To reduce the number of containers in the cluster  
- [x] To provide an abstraction layer that simplifies container orchestration  
- [x] To allow containers in the same Pod to share networking and storage resources  
- [ ] To enable Pods to run on multiple nodes simultaneously  

---

## Question 9

Which Kubernetes component ensures that the desired state of the cluster is maintained?  
- [x] Kube Controller Manager  
- [ ] Kube Proxy  
- [ ] etcd  
- [ ] Kubelet  

---

## Question 10

What is the primary function of etcd in Kubernetes architecture?  
- [ ] Scheduling pods on worker nodes  
- [ ] Running controllers for cluster operations  
- [ ] Handling container runtime  
- [x] Storing all cluster data, including state and configuration  
---
