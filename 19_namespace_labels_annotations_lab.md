# **Working with Labels, Namespaces, and Annotations in Kubernetes**

## **Lab Overview**

In this lab, you will get hands-on experience with **Labels**, **Namespaces**, and **Annotations** in Kubernetes. You will learn how to:

1. Apply and use Labels to organize resources.
2. Create and manage Namespaces to isolate resources.
3. Add and view Annotations to store metadata on resources.

## **Pre-requisites**

- A running Kubernetes cluster (either local using Minikube or in the cloud).
- **kubectl** installed and configured to interact with the cluster.

## **Outcomes**

By the end of this lab, you will be able to:

- Create Kubernetes resources with Labels and select resources using labels.
- Organize resources into Namespaces.
- Use Annotations to store non-identifying metadata on Kubernetes resources.


## **Description**

In this guided lab, you will apply Labels to Pods, create and switch between different Namespaces, and use Annotations for adding extra metadata to Pods. You will also perform tasks that require labeling, namespaces, and annotations, which are crucial for organizing and managing resources in a Kubernetes environment.


## **TASKS**

### **Task 1: Create a Pod with a Label**

**Objective**: Create a Pod with a label and list all Pods with that label.

**Step 1**: First, create a Pod with a label in your default namespace using the following YAML definition:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

**Step 2**: Apply the YAML definition to create the Pod:

```bash
kubectl apply -f nginx-pod.yaml
```

**Step 3**: Verify the Pod creation:

```bash
kubectl get pods
```

**Step 4**: Now, list Pods using the label `app=nginx`:

```bash
kubectl get pods -l app=nginx
```

**Step 5**: Delete this Pod:

```bash
kubectl delete pod nginx-pod
```

### **Task 2: Create a Namespace and Deploy Resources into it**

**Objective**: Create a new Namespace and deploy resources within it.

**Step 1**: Create a new namespace `dev`:

```bash
kubectl create namespace dev
```

**Step 2**: Now, deploy the same `nginx-pod.yaml` in the `dev` namespace. Modify the YAML file to add the `namespace` field:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  namespace: dev
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx
```

**Step 3**: Apply the updated YAML file:

```bash
kubectl apply -f nginx-pod.yaml
```

**Step 4**: List Pods in the `dev` namespace:

```bash
kubectl get pods -n dev
```

**Step 5**: Verify that the Pod is only present in the `dev` namespace and not in the default namespace.

```bash
kubectl get pods
```

### **Task 3: Adding Annotations to Pods**

**Objective**: Add annotations to your Pods for storing metadata.

**Step 1**: Modify the existing `nginx-pod.yaml` file to add annotations. Here’s an example of adding a description annotation to the Pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  namespace: dev
  labels:
    app: nginx
  annotations:
    description: "This is an nginx pod in the dev namespace."
spec:
  containers:
  - name: nginx
    image: nginx
```

**Step 2**: Apply the YAML file with the annotation:

```bash
kubectl apply -f nginx-pod.yaml
```

**Step 3**: Verify the annotations by describing the Pod:

```bash
kubectl describe pod nginx-pod -n dev
```

Look for the **Annotations** section in the output, which should display the `description` annotation you added.

### **Task 4: Clean Up Resources**

**Objective**: Clean up the resources you created during the lab.

**Step 1**: Delete the Pod from the `dev` namespace:

```bash
kubectl delete pod nginx-pod -n dev
```

**Step 2**: Delete the `dev` namespace:

```bash
kubectl delete namespace dev
```


## **Submission Guidelines**

1. Make sure all the steps in the lab have been followed.
2. Provide screenshots or terminal outputs showing the results of each task.
3. Submit a ZIP file containing the following:
   - YAML files used during the lab.
   - Any command-line outputs (screenshots or text) showing the results of the tasks.

Make sure the file is shared with access to anyone as viewer.

## **Additional Resources**

- [Kubernetes Documentation on Labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)
- [Kubernetes Documentation on Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)
- [Kubernetes Documentation on Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)
