# Scaling Applications

## Overview

In this lesson, you will learn about Scaling Applications in Kubernetes. Kubernetes offers ways for manual or automatic scalability.

## Lesson Outcomes

By the end of this lesson, you will be able to:

- Understand the need for scaling applications in Kubernetes.
- Be able to control and reconfigure Horizontal Pod Autoscaling (HPA) so it can autonomously scale applications based on resources consumed or available.

## Explanation

### Why Scale Applications?

Technically, the primary point of scaling applications is that you can provide more resources and ensure that your service can deal with load increases. If replicas of your application are too less or too many, your service might have problems, including being slow or unavailable. In case of replicas, either running too low or running too high, you risk losing money and resources unnecessarily.

### Types of Scaling in Kubernetes

1. **Manual Scaling**: You manually let the number of Pods (replicas) of your application to be run. This one is more practical when you can precisely predict the demand and you are sure of the load to expect.

2. **Automatic Scaling (Horizontal Pod Autoscaling)**: Kubernetes can automatically adjust the number of Pods based on "resource utilization," like CPU or memory usage.

3. **Vertical Scaling**: It involves the dynamic provision or removal of compute resources (CPU and memory) made available to a workload as it operates, and is one of the family of autoscaling techniques that can be used in Kubernetes.

### Manual Scaling with Kubectl

To scale your application manually, use the `kubectl scale` command. This is useful when you want to ensure that a specific number of replicas are running at all times.

#### Example: Scaling a Deployment

Let's say you have a Deployment for a web application, and you want to scale it to 5 replicas. Use the following command:

```bash
kubectl scale deployment <deployment-name> --replicas=5
```

For example, to scale the `nginx-deployment` to 5 replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

This command will ensure that 5 Pods are running for the `nginx-deployment`. You can confirm the scaling by running:

```bash
kubectl get deployments
```

### Horizontal Pod Autoscaling (HPA)

**Horizontal Pod Autoscaling (HPA)** allows Kubernetes to automatically adjust the number of Pods based on CPU, memory, or custom metrics. HPA helps your application handle traffic spikes and conserve resources during low demand.

#### Prerequisites for HPA:
1. **Metrics Server**: Ensure the Metrics Server is installed in your cluster. It collects resource usage data (like CPU and memory) for Pods.

   Install the Metrics Server if it's not already set up:
   ```bash
   kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
   ```

2. **Resource Requests and Limits**: For HPA to work, your Pods must define resource requests and limits for CPU or memory.

#### Example: Creating an HPA

Let's say you want to create an HPA for a `nginx-deployment` that will scale based on CPU usage. The target CPU utilization is set to 50%.

1. First, ensure your Deployment has resource requests and limits defined. Example YAML for the Deployment:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 2
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
           resources:
             requests:
               cpu: "250m"
               memory: "512Mi"
             limits:
               cpu: "500m"
               memory: "1Gi"
   ```

2. Create the Horizontal Pod Autoscaler:

   ```bash
   kubectl autoscale deployment nginx-deployment --cpu-percent=50 --min=2 --max=10
   ```

   This command tells Kubernetes to:
   - Scale the `nginx-deployment` to maintain 50% CPU utilization.
   - Keep at least 2 replicas running (min).
   - Scale up to a maximum of 10 replicas if needed (max).

3. Check the status of the HPA:

   ```bash
   kubectl get hpa
   ```

   This will display the current CPU usage and scaling status.

#### How HPA Works:

- If CPU utilization exceeds the target (50% in this case), Kubernetes will increase the number of Pods.
- If CPU utilization is lower than the target, Kubernetes will scale down the Pods to save resources.
- HPA is a powerful way to ensure your application can handle varying levels of traffic without manual intervention.

### Monitoring and Optimizing Scaling

To ensure your scaling strategy is effective, it’s important to monitor your applications and adjust scaling policies accordingly.

1. **Monitor Metrics**: Use `kubectl top pods` to view the current CPU and memory usage of your Pods.
   
   ```bash
   kubectl top pods
   ```

2. **Optimize Resource Requests**: Make sure your Pods have accurate resource requests and limits defined. This ensures that HPA has accurate data to work with and prevents Pods from over-consuming resources.

3. **Adjust Scaling Parameters**: If your application’s load changes over time, you may need to adjust the scaling parameters, such as the target CPU utilization or the minimum and maximum number of replicas.

## Suggested Reading

1. **Kubernetes Documentation on Scaling**: [https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#scaling-deployments)
2. **Horizontal Pod Autoscaler in Kubernetes**: [https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/)
