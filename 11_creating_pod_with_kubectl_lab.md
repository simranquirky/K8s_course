# **Creating and Managing Pods with `kubectl` (with Lifecycle Checks)**

## **Lab Overview**

This lab guides you through creating and managing Pods while observing their lifecycle states using `kubectl`. You’ll learn to create a Pod, monitor its transitions, simulate failures, and clean up resources.

---

## **Pre-requisites**

1. A running Kubernetes cluster.
2. `kubectl` installed and configured.
3. Familiarity with Pod lifecycle phases (Pending, Running, Succeeded, Failed).

---

## **Outcomes**

By the end of this lab, you will:

- Create and manage Pods using `kubectl`.
- Observe Pod lifecycle transitions and understand their significance.
- Diagnose and investigate Pod issues.

---

## **Tasks**

### **Task 1: Create a Pod and Observe Lifecycle States**

---

### **Step 1.1: Create the Pod**

Run the following command to create a Pod:

```bash
kubectl run my-nginx --image=nginx -restart=Never
```

**What it does:**

- `kubectl run`: A `kubectl` command to quickly create Pods.
- `my-nginx`: The name of the Pod you’re creating.
- `-image=nginx`: Specifies the container image to run inside the Pod (here, the official NGINX image).
- `-restart=Never`: Ensures the Pod is created as a standalone Pod (not part of a Deployment or ReplicaSet)

---

### **Step 1.2: Check the Pod’s Initial State**

Run this command to check the status of the Pod:

```bash
kubectl get pods

```

**What it does:**

- Lists all the Pods in the current namespace.
- Displays key details like Pod name, current state (`Pending`, `Running`, etc.), and uptime.

**What to observe:**

- After creation, the Pod might appear as `Pending` or `ContainerCreating`.
- This indicates Kubernetes is setting up resources like pulling the container image.

---

### **Step 1.3: Watch the Pod Transition to Running**

Monitor the Pod’s status in real time:

```bash
kubectl get pods --watch

```

**What it does:**

- `-watch`: Continuously refreshes the Pod’s status until you stop it manually (`Ctrl+C`).
- Shows the transition from `Pending`, `ContainerCreating` to `Running` as Kubernetes prepares the container.

---

### **Task 2: Simulate Pod Failures and Observe Lifecycle**

### **Step 2.1: Force a Pod Failure**

Simulate a failure by stoping the NGINX server running inside the my-nginx Pod:

```bash
kubectl exec my-nginx -- nginx -s stop
```

**What it does:**

- `kubectl exec`: Executes a command inside the running container of the Pod.
- `my-nginx`: Specifies the target Pod.
- `--`: Indicates the start of the actual command to run inside the container.
- `nginx -s stop`: It sends a stop signal to the NGINX process running inside the container.

---

### **Step 2.2: Observe the Pod’s State**

Check the Pod’s status again:

```bash
kubectl get pods --watch
```

**What it does:**

- Displays the current state of the Pod.
- The Pod might enter `Completed` or `CrashLoopBackOff` if it keeps restarting due to the simulated failure.

---

### **Step 2.3: Investigate the Failure**

Get detailed information about the Pod:

```bash
kubectl describe pod my-nginx
```

**What it does:**

- `kubectl describe`: Provides a detailed description of the specified resource.
- `pod my-nginx`: Specifies the Pod to describe.
- Includes information such as:
    - Events (e.g., errors or warnings).
    - Container logs.
    - Resource usage and limits.

**What to observe:**

- Look for events and error messages that explain why the Pod is failing.

---

### **Task 3: Clean Up and Observe Final States**

### **Step 3.1: Delete the Pod**

Clean up the Pod after completing the tasks:

```bash
kubectl delete pod my-nginx
```

**What it does:**

- Deletes the specified Pod from the cluster.
- Kubernetes removes the Pod and its associated resources.

### **Step 3.2: Verify the Deletion**

Confirm the Pod is deleted:

```bash
kubectl get pods
```

**What it does:**

- Displays the current list of Pods.
- The Pod `my-nginx` should no longer appear in the output.

---

## **Submission Guidelines**

1. Submit a screenshot of the Pod’s status transitions (e.g., `Pending` → `Running`).
2. Submit the output of the `kubectl describe pod my-nginx` command showing the failure event.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources

- [Kubectl run](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_run/)