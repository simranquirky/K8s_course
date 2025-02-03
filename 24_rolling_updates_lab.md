# **Rolling Updates and Update Strategies**

## **Objective:**  
In this lab, you will perform a rolling update on an existing deployment, explore update strategies (default rolling, recreate), and manage the process using `kubectl`. You will also learn how to perform a rollback if needed.

## **Pre-requisites**
- A running Kubernetes cluster with basic knowledge of deployments.
- Familiarity with `kubectl` commands.

## **Outcomes**
By the end of this lab, you will:
- Perform a rolling update on a Kubernetes Deployment.
- Use and understand different update strategies.
- Rollback a deployment to a previous version.

### **Task 1: Create a Basic Deployment**

**Step 1: Create a simple Kubernetes Deployment**  
- Create a `deployment.yaml` file for a simple application (e.g., Nginx or any basic app) with a specific version of an image.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
        - name: webapp
          image: nginx:1.14.2
          ports:
            - containerPort: 80
```

**Step 2: Apply the Deployment to your Cluster**  
Run the following command to create the deployment:

```bash
kubectl apply -f deployment.yaml
```

**Step 3: Verify the Deployment**  
Check if the pods are created and running:

```bash
kubectl get pods
```

### **Task 2: Perform a Rolling Update**

**Step 1: Update the Deployment**  
Now, update the Nginx version by modifying the image in the `deployment.yaml` file (e.g., change `nginx:1.14.2` to `nginx:1.16.0`).

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
        - name: webapp
          image: nginx:1.16.0
          ports:
            - containerPort: 80
```

**Step 2: Apply the New Version**  
Run the following command to apply the updated deployment:

```bash
kubectl apply -f deployment.yaml
```

**Step 3: Monitor the Rolling Update**  
Use `kubectl rollout status` to monitor the update process:

```bash
kubectl rollout status deployment/webapp-deployment
```

You can use `kubectl get pods --watch` to observe the status of the pods.

### **Task 3: Change the Update Strategy to "Recreate"**

**Step 1: Modify the Deployment Strategy**  
Now, modify the deployment to use the **Recreate** strategy and modifying the image (e.g., change `nginx:1.16.0` to `nginx:1.21.0`). This will delete all pods and create new ones, causing downtime during the update.

Update the `deployment.yaml` file as follows:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: webapp-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: webapp
  template:
    metadata:
      labels:
        app: webapp
    spec:
      containers:
        - name: webapp
          image: nginx:1.21.0
          ports:
            - containerPort: 80
  strategy:
    type: Recreate
```

**Step 2: Apply the New Strategy**  
Run the command again to apply the new strategy:

```bash
kubectl apply -f deployment.yaml
```

**Step 3: Observe the Recreate Strategy**  
Watch how the pods are deleted and recreated. You can use `kubectl get pods --watch` to observe the status of the pods.

### **Task 4: Rollback the Update**

**Step 1: Rollback the Deployment to the Previous Version**  
If something went wrong with the update, you can roll back to the previous version of the deployment. Run the following command:

```bash
kubectl rollout undo deployment/webapp-deployment
```

**Step 2: Verify the Rollback**  
Check the pod status to verify that the previous version has been restored:

```bash
kubectl get pods
```

### **Task 5: Cleanup**

**Step 1: Delete the Deployment**  
Once you’ve completed the tasks, clean up your resources by deleting the deployment:

```bash
kubectl delete deployment webapp-deployment
```

## **Submission Guidelines**
1. Submit the output of the commands you used for rolling updates, and rollbacks.
2. Describe the update strategy you applied and any issues you encountered.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## **Additional Resources**
- [Kubernetes Rolling Update Documentation](https://kubernetes.io/docs/tutorials/kubernetes-basics/update-update/)
- [Deployment Strategies](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-strategies)
- [Rolling Update Troubleshooting](https://kubernetes.io/docs/tutorials/kubernetes-basics/update-update/)


