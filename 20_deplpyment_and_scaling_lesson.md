
# **Deployments and Scaling in Kubernetes**

## **Overview**

To be sure that your application is working impeccably, you have to manage the daily or life-cycle of the applications. . At this time we spotlight Deployments, which are a way of managing the state of your application, and scaling it. Additionally, we will explore when deployments are necessary, what they are, and scaling methods-used to satisfy the resource requirements of the application when the traffic or the application load changes.

## **Lesson Outcomes**

After finishing this lesson, you should be able to do the following:

- Determine what Deployments are in Kubernetes and how they are used to manage a set of Pods automatically.
- Experiment with the following operations: create, update, and rollback Deployments.
- Get to the bottom of the concept of Scaling in Kubernetes and the tools that are used for the scaling of Pods.
- See the mechanism of scaling in Kubernetes and get familiar with the error detection and handling by Kubernetes when the application is being scaled.

## **Explanation**

### **Why Do We Need Deployments in Kubernetes?**

In the absence of Deployments, you will be forced to go through a very tough and tedious process trying to get your application right with updates, scaling, and rollbacks. The core problem was that prior to Deployments, the burden of maintaining pods was on our shoulders, which would result in situations such as the application running in inconsistent states, downtime, and update management difficulties.

#### **Deployments bring the extended possibilities like**:

1. **Declarative Updates**: You can define in a Deployment not only the current state and the desired state of the application but also it will make Kubernetes shift the application to the desired state (if there is any) by latest app reconfiguration. For instance, you can now have 3 copies of a Pod running parallel, and the Deployment will see to it that the three Pods are still running after any scaling or rolling update.

2. **Rolling Updates and Rollbacks**: Deployments allow you to roll out new versions of your application without facing any downtime. Even if something goes wrong, Kubernetes can automatically revert it back to the older version.

3. **Self-Healing**: Kubernetes can handle it automatically by replacing the crashing or deleted Pod in the Deployment with a new one to keep the wanted number of Pods.

4. **Declarative Configuration**: Only the desired state of the app can be specified with Deployments, and Kubernetes itself does the rest of the job to make the app what you want.

### **What is a Deployment in Kubernetes?**

A **Deployment** in Kubernetes is a high-level abstraction that coordinates the management of Pods as well as ReplicaSets. It is an automated process of management that involves the scaling, updating, and ensuring the availability of your application. You create a Deployment using YAML and Kubernetes takes care that the right number of Pods are running and that any changes, if needed (for example, to the application, or scaling) are applied correctly.

#### Key features of Deployments:
- **Replica Management**: The Component in Question is in charge of the pod instances number (the maximum and minimum the system can run simultaneously).
- **Rolling Updates**: Implement a method to maximize your service availability during updates by replacing the old Pods with the new version the ones.
- **Rollback**: Kubernetes saves Deployment history by itself and gives you the ability to go back to the previous version if a problem occurs.
- **Pod Template**: A Deployment includes a Pod template, which basically is a blueprint for the Pods it manages.

### **How to Create a Deployment in Kubernetes**

It is possible to create a Deployment through `kubectl` also through a YAML file. Here is a simple YAML definition for a Deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

#### Breakdown:
- **apiVersion**: The version of the API used for this object. In the case of Deployments, generally, it is `apps/v1`.
- **kind**: Specifies the type of object; in this case, a `Deployment`.
- **metadata**: The name and other metadata for the Deployment.
- **spec**: Defines the desired state for the Deployment.
  - **replicas**: Number of replicas (Pods) you want to run.
  - **selector**: A label selector to match Pods for this Deployment.
  - **template**: Describes the Pod template, which includes container details like the image to run.

### **Scaling Applications in Kubernetes**

Scaling in Kubernetes is a key component in creating elasticity in shipping work. You would be able to add or remove replicas based on the demand of your application that's the scaling in Kubernetes feature.

#### **Why is Scaling Important?**

Scaling helps you:
- **Handle increased load**: In case of additional Inbound traffic, increase the number of Pods.
- **Optimize resource utilization**: When the traffic load is low, you can shut down the service to save the resources.
- **Maintain availability**: If some Pods fail, Kubernetes can automatically reschedule new Pods to replace them.

#### **How to Scale Applications in Kubernetes**

You don't have to worry about the scaling out of your applications using `kubectl`. You can always change the number of replicas in your Deployment YAML file for eg.

**Using `kubectl`**:
```bash
kubectl scale deployment my-app-deployment --replicas=5
```
This command scales the Deployment `my-app-deployment` to 5 replicas.

**Modifying the YAML**:
You can also edit the YAML file to change the number of replicas and then apply the new configuration:
```bash
kubectl apply -f deployment.yaml
```

### **Rolling Updates and Rollbacks**

One of the most powerful features of Deployments is the ability to perform rolling updates and rollbacks.

- **Rolling Updates**: This is the process of gradually replacing Pods with a new version without downtime. Instead of stopping all the pods at the same time, Kubernetes makes sure that a certain number of them will be updated at a time. Thus, the application stays available.

- **Rollbacks**: Suppose there is a problem that occurred after the application update, which means that the system needs to be downgraded to the previous version. In this case, Kubernetes can roll the version back automatically.
  
To trigger a rollback:
```bash
kubectl rollout undo deployment/my-app-deployment
```

### **Key Takeaways**
- **Deployments** are crucial in cloud computing, they are not only machines but a team that can manage the desired state of your application as well as scale, update, and ensure that services are always available.
- **Scaling** enables the pods to be adjusted to meet the changing nature of the business by changing the number of Pods that are running.
- **Rolling Updates** are potential to bring the new versions into production without crashing the running old versions. Apart from this, the **Rollbacks** mobile app can be used as a purpose for the action of the rolling back method if the latter is necessary.


## **Suggested Reading**
1. [Kubernetes Deployments Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
2. [Kubernetes Scaling Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-a-deployment)

