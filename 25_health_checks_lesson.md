# **Health Checks in Kubernetes**

## **Overview**
Health checks become inevitable for the maintenance of the solidity and reliability of applications running in Kubernetes. It aids Kubernetes in observing the states of Pods as well as confirming that the Pods are working properly. The lesson starts by looking into instances where health checks are extremely crucial and then moves to the types of health checks Kubernetes provides.


## **Lesson Outcomes**
By the end of this lesson, you will be able to:
1. Narrow down the cases in which health checks are needed.
2. Grasp the types of health checks that are in the Kubernetes environment and their roles in maintaining the system.
3. Liveness, Readiness and Startup Probes Configuration
4. Use `kubectl` commands to verify and troubleshoot health checks.


## **Explanation**

Let us first try to know the importance of health checks through different scenarios:
### **Scenarios Where Health Checks Are Essential**
1. **Application Crashes**  
   Let's say an application running in a Pod crashes a few seconds after it is deployed due to an unexpected bug. How would Kubernetes notice this fault? If this did not happen, the Pod would not be healthy due to an error in the system.

2. **Application Overload**  
   You have a situation here where traffic load is heavier than normal and the application becomes unresponsive. Kubernetes may be routing the traffic to the Pod that's overloaded, henceforth, the requests will fail and so user experience will be negatively affected even if it’s not aware that it's happening.

3. **Initialization Failures**  
   Some applications need a certain amount of time to start or require certain dependencies to be present before they become operational. Not using health checks, Kubernetes may send the traffic to the pods before they are ready, hence causing errors.

4. **Gradual Degradation**  
   An application is likely to have (e.g. memory leaks) if it is left on. If it does not obtain health checks, Kubernetes will never know that it needs a restart.

Above scenarios highlight the need for health checks to maintain application stability and a seamless user experience.

### **Types of Health Checks in Kubernetes**
Kubernetes implements health checks through **Probes** . Each probe fulfills a different purpose, and they apply to the mentioned scenarios below:

1. **Liveness Probe**  
   - **Purpose**: Detects if the application is alive (not crashed).  
   - **Action**: Restarts the container if the check fails.  
   - **Use Case**: Recover from application crashes or unexpected termination.

2. **Readiness Probe**  
   - **Purpose**: Determines if the application is ready to serve requests.  
   - **Action**: Removes the Pod from load balancing until it becomes ready.  
   - **Use Case**: Handle initialization delays or temporary resource issues.

3. **Startup Probe**  
   - **Purpose**: Ensures the application has completed its startup process.  
   - **Action**: Prevents Liveness and Readiness Probes from running until the application is ready.  
   - **Use Case**: Useful for apps with long or unpredictable startup times.

### **How Health Checks Work**
Health checks use **Probes**, which perform periodic checks on the container. Kubernetes supports three mechanisms for probing:

1. **HTTP Probes**  
   - Sends an HTTP request to a specified endpoint.  
   - Example: `/healthz`.  

2. **TCP Probes**  
   - Attempts to establish a TCP connection on a specified port.  
   - Example: Used for services like databases.

3. **Command Probes**  
   - Executes a command inside the container and checks the exit code.  
   - Example: Useful for custom scripts or app-specific checks.

### **Configuring Health Checks in YAML**
Here’s an example of configuring all three probes for an NGINX container:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.21.0
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /healthz
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    readinessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
    startupProbe:
      httpGet:
        path: /startz
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
```

**Key Parameters**:  
- `initialDelaySeconds`: Time to wait before starting the probe.  
- `periodSeconds`: Frequency of the probe checks.  
- `httpGet`: Specifies the HTTP endpoint for the health check.  

### **Monitoring Health Checks**
- Check Pod status:  
  ```bash
  kubectl get pods
  ```
- Describe Pod for detailed probe information:  
  ```bash
  kubectl describe pod <pod-name>
  ```
- View Pod logs:  
  ```bash
  kubectl logs <pod-name>
  ```


### **Best Practices for Health Checks**
1. Use **Liveness Probes** sparingly; only when you expect your application to recover after a restart.  
2. Set reasonable values for `initialDelaySeconds` to avoid false negatives during startup.  
3. Use **Readiness Probes** to handle temporary issues like high latency or resource contention.  
4. Test your health checks thoroughly to ensure they accurately reflect the application state.

## **Suggested Reading**
- [Health Check Best Practices](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)
- [Kubernetes Probes Documentation](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)
- [Debugging Pods](https://kubernetes.io/docs/tasks/debug/debug-application/)

