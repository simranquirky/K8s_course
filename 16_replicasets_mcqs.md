# MCQs: Replica Controllers and Replica Sets

## **Overview**

This quiz assesses your understanding of Replication, ReplicaSets, and ReplicaControllers in Kubernetes.


## **Learning Objectives**

By the end of this quiz, you should be able to:

- Understand the concepts of Replication, ReplicaSets, and ReplicaControllers.
- Identify the differences and use cases for each.


## Question 1 

**What is the main purpose of a Replica Controller in Kubernetes?**

- [ ] A) To manage the lifecycle of individual Pods  
- [x] B) To ensure a specified number of identical Pods are running at all times  
- [ ] C) To manage Kubernetes Nodes  
- [ ] D) To handle rolling updates of applications  

## Question 2

**Which of the following is a key limitation of Replica Controllers?**

- [ ] A) They cannot scale Pods automatically  
- [x] B) They do not support the use of specific label selectors for Pods  
- [ ] C) They can only scale Pods up, not down  
- [ ] D) They do not maintain application availability  

## Question 3

**What is the primary role of a Replica Set in Kubernetes?**

- [ ] A) To handle network traffic routing  
- [x] B) To ensure the desired number of Pods are running and can handle label selectors  
- [ ] C) To manage the storage volumes in a cluster  
- [ ] D) To monitor the cluster's performance  

## Question 4

**Which feature differentiates Replica Sets from Replica Controllers?**

- [ ] A) The ability to perform rolling updates  
- [x] B) Support for label selectors and matching Pods with specific labels  
- [ ] C) The ability to create Pods from scratch  
- [ ] D) The integration with Kubernetes API Server  

## Question 5

**How does a Replica Set scale Pods?**

- [ ] A) It manually triggers Pod scaling based on user input  
- [ ] B) By adjusting the resource requests and limits of Pods  
- [x] C) It watches the cluster for changes, then creates or deletes Pods to match the desired number  
- [ ] D) It uses horizontal pod autoscalers to automatically scale based on load  

## Question 6

**What is the role of labels in a Replica Set?**

- [ ] A) They define the configuration of Pods within a Replica Set  
- [ ] B) They are used to manage the deployment configurations  
- [x] C) Labels help in selecting and managing Pods for scaling or replication  
- [ ] D) They are used to monitor cluster health  

## Question 7

**When would you consider using a Replica Set directly?**

- [x] A) When you want to manage Pods with specific labels without needing rolling updates  
- [ ] B) When you need to manage a set of Nodes  
- [ ] C) When you want to deploy applications using Helm charts  
- [ ] D) When you want to handle multi-cloud deployments  

## Question 8

**Which of the following is a major difference between Replica Controllers and Replica Sets?**

- [ ] A) Replica Sets support rolling updates, whereas Replica Controllers do not  
- [ ] B) Replica Controllers use labels, while Replica Sets do not  
- [x] C) Replica Controllers are used within Deployments, while Replica Sets are not  
- [ ] D) Replica Sets are more flexible and support label selectors, while Replica Controllers are limited in this area  

## Question 9

**What is the main use of a Deployment in Kubernetes?**

- [ ] A) To manage networking configurations  
- [x] B) To manage the lifecycle and updates of Replica Sets  
- [ ] C) To monitor the health of nodes in the cluster  
- [ ] D) To create persistent storage volumes  

## Question 10  

**What does a Replica Set do when a Pod with a matching label already exists in the cluster?**

- [ ] A) It deletes the Pod to maintain the desired number of Pods  
- [ ] B) It ignores the Pod and creates a new one  
- [x] C) It adopts the existing Pod as part of the Replica Set  
- [ ] D) It updates the configuration of the existing Pod  

---
