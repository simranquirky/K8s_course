# Deploy a LoadBalancer Service and Test External Access


## Lab Overview  
In this lab, you will create a Kubernetes service of type `LoadBalancer` to expose a deployment externally. A LoadBalancer service provisions an external load balancer that distributes incoming traffic across the Pods of a service. This is often used in cloud environments where LoadBalancer integrations are supported.



## Pre-requisites  
- A working Kubernetes cluster with a cloud provider that supports LoadBalancer services (e.g., AWS, GCP, Azure).  
- `kubectl` configured to interact with the Kubernetes cluster.  
- Basic knowledge of Deployments and Services in Kubernetes.  



## Outcomes  
By the end of this lab, you will:  
1. Deploy a sample application in a Kubernetes cluster.  
2. Create a LoadBalancer service to expose the application.  
3. Access the application using the external load balancer.  



## Description  
The `LoadBalancer` service type is used to expose applications to the internet by integrating with the underlying cloud provider's load balancing service. It automatically assigns an external IP to the service, making it accessible outside the cluster.  

In this lab, you will:  
1. Deploy a sample application.  
2. Expose the application using a LoadBalancer service.  
3. Test the application using the external IP of the load balancer.  

## TASKS  

### Task 1: Create a Deployment  
Start by creating a deployment for a sample application (e.g., Nginx).  

```bash
kubectl create deployment nginx --image=nginx
```  
- **`kubectl create deployment`**: Creates a deployment.  
- **`nginx`**: The name of the deployment.  
- **`--image=nginx`**: Specifies the container image for the deployment.  

Verify the deployment:  

```bash
kubectl get deployments
```  
- **`kubectl get deployments`**: Lists all deployments in the cluster.  

Check the Pods created by the deployment:  

```bash
kubectl get pods
```  
- **`kubectl get pods`**: Lists the Pods managed by the deployment.  


### Task 2: Expose the Deployment with a LoadBalancer Service  
Create a LoadBalancer service to expose the deployment externally:  

```bash
kubectl expose deployment nginx --type=LoadBalancer --port=80 --target-port=80
```  
- **`kubectl expose deployment`**: Exposes a deployment as a service.  
- **`--type=LoadBalancer`**: Creates a service of type `LoadBalancer`.  
- **`--port=80`**: The port on which the service is exposed.  
- **`--target-port=80`**: The port on the Pods the service forwards traffic to.  

Check the service details:  

```bash
kubectl get svc
```  
- **`kubectl get svc`**: Lists all services in the cluster.  

Look for the `EXTERNAL-IP` column. It may take some time for the load balancer to provision an external IP.

If minikube is running on docker then start the tunnel in another terminal to get the `EXTRENAL-IP`.
```bash
minikube tunnel
```  


### Task 3: Access the Application  
Once the `EXTERNAL-IP` is assigned, use it to access the Nginx application:  

1. Open a web browser and navigate to `http://<EXTERNAL-IP>`.  
2. Alternatively, test using `curl`:  

   ```bash
   curl http://<EXTERNAL-IP>
   ```  
   - **`curl`**: Sends an HTTP request to the external IP of the service.  

You should see the default Nginx welcome page, indicating successful access to the application.  


### Task 4: Clean Up Resources  
To clean up the resources created in this lab, delete the deployment and service:  

```bash
kubectl delete deployment nginx
kubectl delete svc nginx
```  
- **`kubectl delete deployment`**: Deletes the deployment.  
- **`kubectl delete svc`**: Deletes the service.  


## Submission Guidelines  
1. Submit a screenshot or output showing the `LoadBalancer` service with an external IP assigned.  
2. Provide proof of accessing the application using the external IP (e.g., browser screenshot or `curl` output).  

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources  
- [Kubernetes Official Documentation on Services](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)  
- [Kubernetes Deployment Guide](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)  

