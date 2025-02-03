
# **Creating and Managing Replica Sets**

## **Lab Overview**

In this lab, you will learn how to create and manage Replica Sets in Kubernetes. You will understand how to define the number of Pods to maintain, how Replica Sets ensure that the desired number of Pods are running, and how to scale your application using Replica Sets.

## **Pre-requisites**

- A Kubernetes cluster running (local or cloud-based, such as Minikube or Kind).
- `kubectl` command-line tool installed and configured to interact with your Kubernetes cluster.
- Basic understanding of Pods and Labels in Kubernetes.

## **Outcomes**

By the end of this lab, you will:
- Understand how to create a Replica Set using `kubectl`.
- Be able to scale a Replica Set up and down.
- Learn how to monitor the status of your Replica Set.
- Know how to delete a Replica Set and clean up Pods.


## **Description**

Replica Sets ensure that a specified number of identical Pods are running in your Kubernetes cluster. If any Pods fail, the Replica Set will create new ones to maintain the desired count. You will define a Replica Set, interact with it using `kubectl` commands, and observe how it manages your Pods.


## **TASKS**

### **Task 1: Create a Replica Set**

1. **Create a Replica Set using a manifest file** (we’ll use a simple YAML configuration to create the Replica Set).

   - Create a file named `nginx-replicaset.yaml` with the following content:

   ```yaml
   apiVersion: apps/v1
   kind: ReplicaSet
   metadata:
     name: nginx-replicaset
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

   - **Explanation**:
     - `replicas: 3`: This defines that 3 replicas (Pods) should be running at all times.
     - `selector.matchLabels`: Defines the label selector for matching Pods that belong to this Replica Set. Here, it will match Pods with the label `app: nginx`.
     - `template`: Describes the Pods that will be created by the Replica Set. It contains the specifications for the Pods (e.g., the container, image, and port).

2. **Apply the YAML file** using `kubectl` to create the Replica Set:

   ```bash
   kubectl apply -f nginx-replicaset.yaml
   ```

   This will create the Replica Set in your cluster.

### **Task 2: Check the Replica Set and Pods Status**

1. **Check the status of the Replica Set**:

   ```bash
   kubectl get replicasets
   ```

   This command will show you the state of the Replica Set, including the number of Pods currently running.

2. **Check the Pods created by the Replica Set**:

   ```bash
   kubectl get pods -l app=nginx
   ```

   This command lists the Pods that match the label `app=nginx`. You should see 3 Pods running.

3. **Describe the Replica Set for more details**:

   ```bash
   kubectl describe replicaset nginx-replicaset
   ```

   This will provide detailed information about the Replica Set, such as the number of Pods, labels, and the status of the Pods.

### **Task 3: Scale the Replica Set**

1. **Scale the Replica Set to 5 Pods**:

   You can easily scale the Replica Set using the following command:

   ```bash
   kubectl scale replicaset nginx-replicaset --replicas=5
   ```

   This will scale the number of Pods managed by the Replica Set to 5.

2. **Verify the scaling operation**:

   Check the status of the Replica Set and Pods again to confirm that 5 Pods are running:

   ```bash
   kubectl get pods -l app=nginx
   ```

   You should now see 5 Pods.

### **Task 4: Delete a Pod Managed by the Replica Set**

1. **Delete one of the Pods manually**:

   Choose a Pod to delete by using the following command:

   ```bash
   kubectl delete pod <pod-name>
   ```

   Replace `<pod-name>` with the name of one of the Pods that was created by the Replica Set.

2. **Verify the Replica Set recreates the Pod**:

   After deleting the Pod, the Replica Set will automatically create a new Pod to maintain the desired count of 5. You can check this with:

   ```bash
   kubectl get pods -l app=nginx
   ```

   You should see that the total number of Pods has returned to 5.

### **Task 5: Delete the Replica Set**

1. **Delete the Replica Set**:

   If you no longer need the Replica Set, you can delete it using:

   ```bash
   kubectl delete replicaset nginx-replicaset
   ```

2. **Verify that the Pods are deleted**:

   After deleting the Replica Set, the Pods will also be deleted automatically. Check the status of the Pods:

   ```bash
   kubectl get pods -l app=nginx
   ```

   You should see that no Pods are running with the label `app=nginx`.

## **Submission Guidelines**

- Ensure you have followed each step in the lab and that all commands executed successfully.
- Submit the following:
  - The YAML file you created for the Replica Set (`nginx-replicaset.yaml`).
  - Screenshots or terminal logs showing the Replica Set creation, scaling, and Pod management operations.

Note: The screenshots and file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## **Additional Resources**

- [Replica Set Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)
- [Kubernetes Labels and Selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)
