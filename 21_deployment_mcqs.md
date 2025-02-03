# MCQs: Deployments and Scaling in Kubernetes

## **Overview**

This quiz evaluates your understanding of Deployments and Scaling in Kubernetes.

## **Learning Objectives**

By the end of this quiz, you should be able to:

- Understand the concept of Deployments in Kubernetes.
- Comprehend how to scale applications in Kubernetes.

## Question 1

**What is the main purpose of a Deployment in Kubernetes?**

- [ ] A) To manage individual Pods manually  
- [ ] B) To scale the number of Nodes in a Kubernetes cluster  
- [x] C) To automate the management of Pods, including scaling and updates  
- [ ] D) To handle network traffic routing for Pods  

## Question 2

**What is a key feature of Kubernetes Deployments?**

- [ ] A) It automatically creates Persistent Volumes  
- [ ] B) It allows the manual scaling of individual Pods  
- [x] C) It manages rolling updates and rollbacks for Pods  
- [ ] D) It manages the creation of new Kubernetes Nodes  

## Question 3

**What does the `replicas` field in a Deployment YAML file specify?**

- [ ] A) The number of Pods to be deleted  
- [ ] B) The number of containers per Pod  
- [x] C) The number of Pods to run in the Deployment  
- [ ] D) The size of each Pod  

## Question 4

**How does Kubernetes handle Pods that crash or are deleted in a Deployment?**

- [ ] A) It stops the entire Deployment  
- [ ] B) It alerts the user for manual intervention  
- [x] C) It automatically replaces the Pods to maintain the desired number  
- [ ] D) It runs the Pods in a backup environment  

## Question 5

**What is the primary advantage of rolling updates in Kubernetes?**

- [ ] A) It creates new Pods manually  
- [ ] B) It allows applications to run with multiple versions at once  
- [x] C) It ensures that the application remains available during updates  
- [ ] D) It scales the Pods vertically instead of horizontally  

## Question 6

**What command is used to scale a Deployment in Kubernetes?**

- [ ] A) `kubectl scale deployment my-app-deployment --replicas=3`  
- [x] B) `kubectl scale deployment my-app-deployment --replicas=5`  
- [ ] C) `kubectl scale deployment my-app-deployment --replicas=1`  
- [ ] D) `kubectl scale deployment my-app-deployment --cpu=2`  

## Question 7

**What is a Deployment rollback in Kubernetes used for?**

- [ ] A) To permanently delete a Deployment  
- [x] B) To revert to the previous version of an application  
- [ ] C) To change the configuration of a Deployment  
- [ ] D) To increase the resource usage of a Deployment  

## Question 8

**How can you trigger a rollback to the previous version of a Deployment?**

- [ ] A) `kubectl rollback deployment/my-app-deployment`  
- [ ] B) `kubectl update deployment/my-app-deployment`  
- [x] C) `kubectl rollout undo deployment/my-app-deployment`  
- [ ] D) `kubectl undo deployment/my-app-deployment`  

## Question 9

**What is the function of the `selector` field in a Deployment YAML file?**

- [ ] A) It specifies the number of replicas to scale  
- [ ] B) It defines the container image to be used  
- [x] C) It matches the labels of the Pods managed by the Deployment  
- [ ] D) It configures the CPU and memory limits for Pods  

## Question 10  

**What feature allows Kubernetes to update Pods without downtime?**

- [ ] A) Self-Healing  
- [ ] B) Rolling Updates  
- [x] C) Horizontal Pod Autoscaler  
- [ ] D) Vertical Scaling  

---
