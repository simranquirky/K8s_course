# ClusterIP Service - Create and Test ClusterIP Service

## Lab Overview
In this lab, you will create and test a Kubernetes ClusterIP service. The ClusterIP service is the default service type in Kubernetes, and it is used to expose a service inside the cluster, making it accessible only to other resources within the same cluster.

## Pre-requisites
- A working Kubernetes cluster (e.g., Minikube, or any Kubernetes environment).
- `kubectl` configured to interact with the Kubernetes cluster.
- Basic knowledge of Pods in Kubernetes.

## Outcomes
By the end of this lab, you will:
- Understand how ClusterIP services work in Kubernetes.
- Be able to create a ClusterIP service and associate it with a Pod.
- Learn how to test the connectivity to the service within the cluster.

## Description
In Kubernetes, the ClusterIP service type is used to expose a service internally to the cluster. When you create a ClusterIP service, it assigns a virtual IP (VIP) within the cluster to access the service. The service will be accessible only from within the cluster and cannot be accessed externally.

In this lab, you will:
1. Deploy a Pod.
2. Create a ClusterIP service that exposes the Pod.
3. Test connectivity to the ClusterIP service from another Pod.

## TASKS

### Task 1: Create a Pod
First, create a simple Pod running a web server (e.g., Nginx) to expose via the ClusterIP service.

```bash
kubectl run nginx --image=nginx --restart=Never
```
- `kubectl run`: Creates a new Kubernetes Pod.
- `nginx`: The name of the Pod.
- `--image=nginx`: Specifies the Docker image to use for the Pod. In this case, it’s the Nginx image.
- `--restart=Never`: Ensures that the Pod is not part of any ReplicaSet or Deployment.

Verify the Pod is running:

```bash
kubectl get pods
```
- `kubectl get pods`: Lists all the Pods running in your cluster, confirming that the `nginx` Pod is up and running.

### Task 2: Expose the Pod as a ClusterIP Service
Next, create a ClusterIP service that targets the Pod:

```bash
kubectl expose pod nginx --port=80 --target-port=80 --name=nginx-service --type=ClusterIP
```
- `kubectl expose`: This command exposes a resource (in this case, a Pod) as a service.
- `pod nginx`: Specifies that the `nginx` Pod is being exposed as a service.
- `--port=80`: The port the service will listen on.
- `--target-port=80`: The port on the Pod that the service will forward traffic to.
- `--name=nginx-service`: The name of the service being created.
- `--type=ClusterIP`: Specifies that the service type is ClusterIP (default), meaning it is accessible only within the cluster.

Verify the service is created:

```bash
kubectl get svc
```
- `kubectl get svc`: Lists all the services running in the cluster, allowing you to confirm that the `nginx-service` was created and is associated with a ClusterIP.

### Task 3: Test Connectivity to the Service
Now, create another Pod to test the connectivity to the `nginx-service` from within the cluster.

```bash
kubectl run -i --tty test-pod --image=busybox --restart=Never -- /bin/sh
```
- `kubectl run`: Again, this command creates a Pod.
- `-i --tty`: Allows you to interact with the Pod via terminal.
- `test-pod`: The name of the testing Pod.
- `--image=busybox`: Specifies the Docker image for the Pod. In this case, `busybox` is a small Linux container for testing purposes.
- `--restart=Never`: Ensures the Pod is not part of any ReplicaSet or Deployment.
- `-- /bin/sh`: Runs the shell (`sh`) in the `test-pod` so you can interact with it.

Once inside the Pod, test the connection to the service using `wget` or `curl`:

```bash
wget -qO- nginx-service
```
- `wget -qO- nginx-service`: This command attempts to access the `nginx-service` using its ClusterIP. The `-qO-` flag suppresses the output of `wget` and just returns the response from the Nginx service.

You should get a response from the Nginx server running inside the Pod.

To come outside the pod terminal use the `exit` command:
```bash
exit
```

### Task 4: Clean Up Resources
Finally, delete the resources you created to clean up the cluster:

```bash
kubectl delete pod nginx
kubectl delete svc nginx-service
kubectl delete pod test-pod
```
- `kubectl delete pod nginx`: Deletes the `nginx` Pod.
- `kubectl delete svc nginx-service`: Deletes the `nginx-service` ClusterIP service.
- `kubectl delete pod test-pod`: Deletes the test Pod used for checking connectivity.

## Submission Guidelines
1. Submit a screenshot or output showing that the ClusterIP service is created successfully.
2. Provide the output from the test connectivity step showing a successful response from the Nginx service.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources
- [Kubernetes Official Documentation on Services](https://kubernetes.io/docs/concepts/services-networking/service/)
- [Kubernetes ClusterIP Service](https://kubernetes.io/docs/concepts/services-networking/service/#clusterip)

