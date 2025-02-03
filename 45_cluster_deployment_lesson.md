# Cluster Deployments

## Overview

In this lesson, you will learn about the basic explanation of Cluster Deployment technology, which is the main component for distributing applications at scale on the cloud.

## Lesson Outcomes

By the end of this lesson, you will be able to:

- Comprehend the concept of Cluster Deployments in Kubernetes.
- Set up and manage a deployment using `kubectl` and YAML.
- Update and scale the applications where required, as well as rolling update new files.
- Know ReplicaSets like the redundancy of important parts in the applications, thus ensuring the business is operational.

## Explanation

### What is a Cluster Deployment?

A **Cluster Deployment** in Kubernetes is the goal of deploying and running an application across a Kubernetes cluster. It helps your application to run seamlessly and be scalable through using multiple nodes (servers) in a cluster. The Deployment resource is the one Kubernetes utilizes to manage these applications.

#### Key Concepts:

1. **Deployment**: A Kubernetes Deployment is a way to update applications automatically and declaratively. It makes sure the application's intended state is achieved, and solves problems like the insufficient number of pods by restarting the specified number of pods.

2. **ReplicaSet**: As each Deployment is the controller of a set of Pods, it manages to maintain a certain number of its replicas (Pods) and therefore it will always keep running. The ReplicaSet takes adjustment in case of Pods crashing or getting deleted.

3. **Rolling Updates**: Kubernetes Deployments that enable rolling updates make it possible to keep on running your application with little or no downtime. They do this through gradually replacing the previous version of your app with the new one.

4. **Scaling**: You can easily use deployments to horizontally scale the number of replicas (Pods) of an application when demand is high or low. This means a system can be able to deal with more or fewer users in a traffic session.

### How Cluster Deployments Work

In a typical Kubernetes cluster, you use `kubectl` to interact with the Kubernetes API server. When you create a Deployment, Kubernetes takes care of:
- Ensuring the right number of replicas are running.
- Monitoring the health of the application.
- Automatically updating or rolling back your application when needed.

### Steps for Creating a Cluster Deployment

1. **Create a Deployment YAML file**: This file defines the desired state of your application, such as the container image to use, the number of replicas, and other configurations like environment variables or port bindings.

   Example of a basic deployment YAML file (`nginx-deployment.yaml`):
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         labels:
           app: nginx
       spec:
         containers:
         - name: nginx
           image: nginx:latest
           ports:
           - containerPort: 80
   ```

2. **Apply the Deployment**: Use the `kubectl apply` command to create or update the Deployment:
   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```

3. **Check the Status**: Use the following command to check the status of the Deployment:
   ```bash
   kubectl get deployments
   ```

4. **Scaling the Deployment**: You can scale the number of replicas of your deployment as per your application needs:
   ```bash
   kubectl scale deployment nginx-deployment --replicas=5
   ```

5. **Rolling Updates**: When you want to update your application, you can modify the Deployment YAML file (e.g., change the container image version) and apply the updated file:
   ```bash
   kubectl apply -f updated-nginx-deployment.yaml
   ```

   Kubernetes will handle rolling updates by gradually replacing the old version of the application with the new one.

6. **Rollback**: If something goes wrong with the update, Kubernetes allows you to roll back to the previous version:
   ```bash
   kubectl rollout undo deployment/nginx-deployment
   ```

7. **Deleting a Deployment**: When you want to delete the Deployment, use the following command:
   ```bash
   kubectl delete deployment nginx-deployment
   ```

### Benefits of Cluster Deployments

1. **High Availability**: Kubernetes ensures your application is always running by maintaining the desired number of replicas. If a Pod fails, it will automatically replace it.
  
2. **Scalability**: You can scale your application easily by adjusting the number of replicas based on the load.

3. **Zero-Downtime Updates**: Rolling updates allow you to update your application without downtime.

4. **Self-Healing**: Kubernetes automatically handles failures and restarts Pods if they crash.

## Suggested Reading

1. **Kubernetes Documentation on Deployments**: [https://kubernetes.io/docs/concepts/workloads/controllers/deployment/](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
2. **Scaling Deployments in Kubernetes**: [https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/)
3. **Rolling Updates in Kubernetes**: [https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/](https://kubernetes.io/docs/tutorials/kubernetes-basics/update/update-intro/)
