
# **Deployments and Scaling in Kubernetes**

## **Lab Overview**
In this lab, you will work with Kubernetes Deployments and explore how to scale your application to handle varying loads. You will create a deployment, scale it up, and manage the number of replicas in the cluster.

## **Pre-requisites**
- A running Kubernetes cluster (Minikube, Kind, or managed Kubernetes service).
- Familiarity with `kubectl`.

## **Outcomes**
By the end of this lab, you will:
- Deploy an application using a Kubernetes Deployment.
- Scale the deployment up or down.
- Monitor Pods and their statuses after scaling.

## **Description**
This lab provides a hands-on experience with Kubernetes deployments. You will create a simple application, scale it horizontally, and verify that Kubernetes manages the scaling process as expected.

### **TASK 1: Create a Kubernetes Deployment**
1. Create a new NGINX deployment with the following command:
   
   ```bash
   kubectl create deployment nginx --image=nginx:1.21.0
   ```

2. Verify the deployment is created:
   
   ```bash
   kubectl get deployments
   kubectl get pods
   ```

3. Describe the deployment to check its configuration:
   
   ```bash
   kubectl describe deployment nginx
   ```

### **TASK 2: Scale the Deployment**
1. Use `kubectl scale` to increase the number of replicas from 1 to 3:

   ```bash
   kubectl scale deployment nginx --replicas=3
   ```

2. You should see 3 pods running instead of just 1. Verify the scaling operation:

   ```bash
   kubectl get pods
   kubectl describe deployment nginx
   ```

### **TASK 3: Scale the Deployment Down**
1. Reduce the number of replicas to 2:
   
   ```bash
   kubectl scale deployment nginx --replicas=2
   ```

2. You should see only 2 pods running now. Verify the scaling down operation:

   ```bash
   kubectl get pods
   kubectl describe deployment nginx
   ```

### **TASK 4: Clean Up Resources**
1. Delete the NGINX deployment:
   
   ```bash
   kubectl delete deployment nginx
   ```

## **Submission Guidelines**
1. Provide the output of the commands you used to scale the deployment.
2. Include any observations regarding how scaling works and how Kubernetes handles pod creation and removal.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## **Additional Resources**
- [Kubernetes Deployments Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
- [Kubernetes Scaling Documentation](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)

