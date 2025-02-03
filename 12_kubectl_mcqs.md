
# **MCQs: Mastering kubectl Commands**  

## **Overview**

This quiz tests your knowledge of key concepts and commands related to `kubectl`, the command-line tool for managing Kubernetes.


## **Learning Objectives**

By the end of this quiz, you should be able to:

- Understand the purpose and functionality of `kubectl`.
- Identify correct syntax and use cases for `kubectl` commands.
- Inspect, debug, and manage resources with `kubectl`.


## Question 1  

Which command is used to create Kubernetes resources from a YAML or JSON file?  
- [ ] `kubectl get`  
- [ ] `kubectl describe`  
- [x] `kubectl apply`  
- [ ] `kubectl delete`  

---

## Question 2  

What does the `kubectl get pods` command do?  
- [ ] Deletes all pods in the current namespace  
- [ ] Creates a new pod  
- [x] Lists all pods in the current namespace  
- [ ] Scales the number of pod replicas  

---

## Question 3  

Which command would you use to view detailed information about a specific Kubernetes resource?  
- [ ] `kubectl create`  
- [x] `kubectl describe`  
- [ ] `kubectl delete`  
- [ ] `kubectl scale`  

---

## Question 4  

What is the primary purpose of `kubectl logs`?  
- [ ] To execute commands inside a running container  
- [ ] To scale the number of replicas in a deployment  
- [x] To view logs from a specific pod  
- [ ] To forward ports from local machine to pod  

---

## Question 5  

How can you delete a specific pod in Kubernetes using `kubectl`?  
- [x] `kubectl delete pod <pod_name>`  
- [ ] `kubectl create pod <pod_name>`  
- [ ] `kubectl scale pod <pod_name>`  
- [ ] `kubectl get pod <pod_name>`  

---

## Question 6  

Which command is used to open an interactive shell within a pod?  
- [ ] `kubectl describe`  
- [ ] `kubectl get`  
- [x] `kubectl exec -it <pod_name> -- /bin/bash`  
- [ ] `kubectl logs <pod_name>`  

---

## Question 7  

What is the main purpose of `kubectl scale`?  
- [ ] To view resource usage statistics  
- [x] To change the number of replicas in a deployment  
- [ ] To view the logs of a pod  
- [ ] To forward ports to a pod  

---

## Question 8  

Which command is used to manage the rollout status of a deployment?  
- [ ] `kubectl scale`  
- [x] `kubectl rollout status deployment <deployment_name>`  
- [ ] `kubectl delete`  
- [ ] `kubectl get`  

---

## Question 9  

How would you edit the configuration of an existing pod using `kubectl`?  
- [ ] `kubectl get pod <pod_name>`  
- [ ] `kubectl delete pod <pod_name>`  
- [x] `kubectl edit pod <pod_name>`  
- [ ] `kubectl create pod <pod_name>`  

---

## Question 10  

What does the `kubectl port-forward` command do?  
- [ ] Deletes a port-forwarding configuration  
- [ ] Creates a new deployment with port forwarding  
- [x] Forwards a local port to a pod  
- [ ] Scales the number of replicas in a pod  

---