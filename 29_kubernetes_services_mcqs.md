# MCQs: Kubernetes Services

## **Overview**

This quiz assesses your understanding of Kubernetes Services, the different types, and their use cases.


## **Outcomes**

By the end of this quiz, you should be able to:

- Understand the different types of Kubernetes Services.
- Identify when to use each type of Service in a Kubernetes cluster.

## Question 1  
What is the primary function of a Kubernetes Service?  
- [x] To provide stable IP addresses or DNS names for Pods and enable efficient communication between them  
- [ ] To manage the lifecycle of Pods  
- [ ] To monitor the health of Pods  
- [ ] To scale Pods dynamically  

## Question 2  
Which type of Kubernetes Service exposes a Service on a static port on every Node’s IP address?  
- [ ] ClusterIP  
- [x] NodePort  
- [ ] LoadBalancer  
- [ ] ExternalName  

## Question 3  
What is the default Service type in Kubernetes?  
- [ ] NodePort  
- [ ] LoadBalancer  
- [x] ClusterIP  
- [ ] ExternalName  

## Question 4  
Which type of Service is typically used for external access with high availability, such as public-facing websites?  
- [ ] ClusterIP  
- [ ] NodePort  
- [x] LoadBalancer  
- [ ] ExternalName  

## Question 5  
In which scenario would you use an ExternalName Service?  
- [ ] To expose services for internal communication within the cluster  
- [ ] To access external resources like an API or database from within the cluster  
- [ ] To provide load balancing for external access  
- [x] To map to an external DNS name  

## Question 6  
What is the main benefit of using Kubernetes Services?  
- [x] They provide stable communication for dynamic Pods  
- [ ] They monitor the health of the Kubernetes cluster  
- [ ] They create persistent storage for Pods  
- [ ] They manage Pods lifecycle directly  

## Question 7  
How does Kubernetes maintain a list of available Pods for a Service?  
- [ ] By assigning a fixed IP address to each Pod  
- [x] Using label selectors to dynamically update the list of endpoints  
- [ ] Through manual configuration by the user  
- [ ] By constantly checking the Pod IP addresses  

## Question 8  
What does a NodePort Service allow you to do?  
- [ ] Access a service within the cluster only  
- [x] Expose a service externally using `<NodeIP>:<NodePort>`  
- [ ] Automatically provision a cloud load balancer  
- [ ] Map a service to an external DNS name  

## Question 9  
Which Service type would be most appropriate for a development environment where external access to the application is required but with minimal complexity?  
- [x] NodePort  
- [ ] LoadBalancer  
- [ ] ExternalName  
- [ ] ClusterIP  

## Question 10  
What is the role of label selectors in Kubernetes Services?  
- [ ] To assign static IP addresses to Pods  
- [ ] To provide DNS names for Pods  
- [x] To identify which Pods should receive traffic based on matching labels  
- [ ] To automatically scale Pods based on traffic load  
