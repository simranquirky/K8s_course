# Scaling Applications with Horizontal Pod Autoscaler (HPA)

## Lab Overview
In this lab, you will configure and observe a Horizontal Pod Autoscaler (HPA) in a Kubernetes cluster running on Minikube. The HPA will scale the number of Pods in a Deployment based on CPU utilization. You will also simulate a workload to see the HPA dynamically adjust the number of Pods.

## Pre-requisites
1. A Windows machine with Minikube installed and running.
2. Kubernetes CLI (`kubectl`) configured and pointing to your Minikube cluster.
3. Metrics Server installed and running in the Minikube cluster.

## Outcomes
By the end of this lab, you will:
- Understand the role of the Metrics Server in Kubernetes.
- Deploy a Kubernetes Deployment and expose it as a Service.
- Configure a Horizontal Pod Autoscaler (HPA) to scale Pods based on CPU usage.
- Observe and analyze the dynamic scaling of Pods based on simulated workloads.

## Description
The lab involves setting up a Kubernetes Deployment and exposing it as a Service. An HPA is then configured to monitor CPU utilization and scale the Deployment's Pods between a defined minimum and maximum count. A stress test tool is used to simulate CPU load, allowing you to observe how the HPA adjusts the number of Pods in real-time.



## TASKS

### Task 1: Install Metrics Server
1. Deploy the Metrics Server:
   ```bash
   kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
   ```
2. Edit the Metrics Server Deployment to add the following arguments under `spec.containers.args`:
   ```yaml
   - --kubelet-insecure-tls
   ```
   Use:
   ```bash
   kubectl -n kube-system edit deployment metrics-server
   ```
3. Restart the Metrics Server:
   ```bash
   kubectl -n kube-system rollout restart deployment metrics-server
   ```
4. Verify Metrics Server functionality:
   ```bash
   kubectl top nodes
   ```



### Task 2: Deploy the Application
1. Create a Deployment YAML file named `deployment.yaml` with the following content:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: hpa-demo
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: hpa-demo
     template:
       metadata:
         labels:
           app: hpa-demo
       spec:
         containers:
         - name: hpa-demo
           image: k8s.gcr.io/hpa-example
           resources:
             requests:
               cpu: 200m
             limits:
               cpu: 500m
   ```
2. Apply the Deployment:
   ```bash
   kubectl apply -f deployment.yaml
   ```



### Task 3: Expose the Application
1. Expose the Deployment as a ClusterIP Service:
   ```bash
   kubectl expose deployment hpa-demo --type=ClusterIP --name=hpa-demo-service --port=80
   ```



### Task 4: Configure Horizontal Pod Autoscaler
1. Create an HPA for the Deployment:
   ```bash
   kubectl autoscale deployment hpa-demo --cpu-percent=50 --min=1 --max=10
   ```
2. Verify the HPA is created successfully:
   ```bash
   kubectl get hpa
   ```



### Task 5: Simulate Load
1. Deploy a stress-testing Pod and, run the following command to generate continuous CPU load:
   ```bash
   kubectl run -it --rm load-generator --image=busybox -- sh -c "while true; do wget -q -O- http://hpa-demo-service; done"
   ```



### Task 6: Observe Scaling
1. Monitor the HPA metrics:
   ```bash
   kubectl get hpa -w
   ```
2. Watch the number of Pods scaling dynamically:
   ```bash
   kubectl get pods -l app=hpa-demo -w
   ```
3. Stop the load-generator using `Ctrl + C`. Monitor the HPA metrics and pods, as pods scale down.



### Task 7: Clean Up
After completing the lab, clean up all the resources:
```bash
kubectl delete deployment hpa-demo
kubectl delete service hpa-demo-service
kubectl delete hpa hpa-demo
kubectl delete pod load-generator
```



## Submission Guidelines
Provide screenshots of the following:
   - HPA status (`kubectl get hpa`).
   - Output of `kubectl top pods`.
   - Logs showing dynamic scaling of Pods.

Note: The screenshots and the file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`


## Additional Resources
- [Kubernetes Horizontal Pod Autoscaler Documentation](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
- [Minikube Official Documentation](https://minikube.sigs.k8s.io/docs/)
- [Metrics Server GitHub Repository](https://github.com/kubernetes-sigs/metrics-server)
