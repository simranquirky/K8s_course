# Deploy a NodePort Service and Test External Access

## Lab Overview
In this lab, you will deploy a Kubernetes NodePort service and test access to the service from outside the cluster. NodePort services are used to expose services externally through a static port on each node in the cluster, enabling external clients to access the service.

## Pre-requisites
- A working Kubernetes cluster (e.g., Minikube, or any Kubernetes environment).
- `kubectl` configured to interact with the Kubernetes cluster.
- Basic knowledge of Pods and Services in Kubernetes.

## Outcomes
By the end of this lab, you will:
- Understand how NodePort services work in Kubernetes.
- Be able to expose a service using NodePort and access it externally.
- Learn how to verify external access to the service.

## Description
In Kubernetes, the NodePort service type exposes a service on a static port across all nodes in the cluster. This enables you to access the service using the IP of any node and the assigned port number.

In this lab, you will:
1. Deploy a Pod.
2. Create a NodePort service.
3. Test access to the service externally using the node's IP address and the assigned port.

## TASKS

### Task 1: Create a Pod
First, create a simple Pod running a web server (e.g., Nginx) to expose via the NodePort service.

```bash
kubectl run nginx --image=nginx --restart=Never
```
- `kubectl run`: Creates a new Kubernetes Pod.
- `nginx`: The name of the Pod.
- `--image=nginx`: Specifies the Docker image for the Pod. In this case, it's the Nginx image.
- `--restart=Never`: Ensures that the Pod is not part of any ReplicaSet or Deployment.

Verify the Pod is running:

```bash
kubectl get pods
```
- `kubectl get pods`: Lists all the Pods running in your cluster, confirming that the `nginx` Pod is up and running.

### Task 2: Expose the Pod as a NodePort Service
Next, create a NodePort service that targets the Pod:

```bash
kubectl expose pod nginx --port=80 --target-port=80 --name=nginx-nodeport --type=NodePort
```
- `kubectl expose`: This command exposes a resource (in this case, a Pod) as a service.
- `pod nginx`: Specifies that the `nginx` Pod is being exposed as a service.
- `--port=80`: The port the service will listen on.
- `--target-port=80`: The port on the Pod that the service will forward traffic to.
- `--name=nginx-nodeport`: The name of the service being created.
- `--type=NodePort`: Specifies that the service type is NodePort, making it accessible externally.

Verify the service is created and note the assigned NodePort:

```bash
kubectl get svc
```
- `kubectl get svc`: Lists all the services in the cluster, including the `nginx-nodeport` service, showing the NodePort assigned.

You should see output similar to this:

```plaintext
NAME               TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
nginx-nodeport     NodePort   10.96.157.231   <none>        80:31380/TCP   2m
```
- The `PORT(S)` column shows the NodePort (`31380` in this case), which is accessible externally.

### Task 3: Access the Service Externally
To test external access, use the external IP of your node. If you are using Minikube, you can get the node's external IP by running:

```bash
minikube ip
```
- `minikube ip`: Returns the IP address of the Minikube VM, which serves as the external IP for accessing services in the cluster.

If you're using another Kubernetes environment (e.g., GKE, EKS), use the public IP of any node in your cluster.

Now, access the service by entering the following URL in your browser or use `curl`:

```bash
curl <node-ip>:<node-port>
```

If the minikube runs on dokcer then use this command to get the exact URL for accessing the nginx-nodeport service:

```bash
minikube service nginx-nodeport --url
```

Open this url in browser. You should receive an HTTP response from the Nginx server running in the Pod, confirming that the NodePort service is successfully exposing the service externally.

### Task 4: Clean Up Resources
Finally, delete the resources you created to clean up the cluster:

```bash
kubectl delete pod nginx
kubectl delete svc nginx-nodeport
```
- `kubectl delete pod nginx`: Deletes the `nginx` Pod.
- `kubectl delete svc nginx-nodeport`: Deletes the `nginx-nodeport` service.

## Submission Guidelines
1. Submit a screenshot or output showing that the NodePort service is created successfully.
2. Provide the output from the external access test showing a successful response from the Nginx service.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources
- [Kubernetes Official Documentation on NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport)
- [Kubernetes Service Types](https://kubernetes.io/docs/concepts/services-networking/service/#service-types)

