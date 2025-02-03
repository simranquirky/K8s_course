
# **Implementing Health Checks in Kubernetes**

## **Objective**
In this lab, you will:
1. Create a Pod with an NGINX container.
2. Configure Liveness, Readiness, and Startup Probes.
3. Test and observe how Kubernetes handles health checks using probes.


## **Prerequisites**
1. A Kubernetes cluster (e.g., Minikube, Kind, or any cloud provider).
2. `kubectl` installed and configured.
3. Basic knowledge of Pods and YAML configurations.

## **Outcomes**
By the end of this lab, you will:
- Be able to Configure Liveness, Readiness, and Startup Probes.

## **Description**
This lab provides a hands-on experience with health checks in Kubernetes.

## **TASKS**

### **Step 1: Create a YAML File for the Pod**
1. Create a new YAML file called `nginx-health-checks.yaml`. Add the following configuration for an NGINX container with Liveness, Readiness, and Startup Probes:
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
           path: /
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
           path: /
           port: 80
         failureThreshold: 30
         periodSeconds: 10
   ```
Save the file.

### **Step 2: Deploy the Pod**
1. Apply the configuration file to your Kubernetes cluster:
   ```bash
   kubectl apply -f nginx-health-checks.yaml
   ```

2. Verify that the Pod is created and running:
   ```bash
   kubectl get pods
   ```

### **Step 3: Simulate Liveness Probe Failures**
1. Simulate a failure by moving the default nginx configuration:
   ```bash
   kubectl exec -it nginx -- /bin/sh -c "mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak"
   kubectl exec -it nginx -- /bin/sh -c "nginx -s reload"
   ```

3. Exit the shell and watch the Pod's behavior:
   ```bash
   kubectl get pods --watch
   kubectl describe pod nginx
   ```
   **Expected Outcome**: Kubernetes will restart the container when the Liveness Probe fails.

### **Step 4: Simulate Readiness Probe Failures**
1. Simulate a Readiness Probe failure by removing the `/` endpoint:
   ```bash
   kubectl exec -it nginx -- /bin/sh -c "mv /usr/share/nginx/html/index.html /usr/share/nginx/html/index-broken.html"
   ```

3. Check the Pod status and endpoints:
   ```bash
   kubectl get pods --watch
   kubectl describe pod nginx
   ```
   **Expected Outcome**: The Pod remains running, but it is removed from the Service load balancer.


### **Step 5: Test Startup Probe**
1. Delete the existing pod:
   ```bash
   kubectl delete pod nginx
   ```

2. Modify the YAML file to introduce a delay in NGINX startup by adding an `args` section:
   ```yaml
       args:
         - /bin/sh
         - -c
         - "sleep 30 && nginx -g 'daemon off;'"
   ```

3. Apply the updated configuration:
   ```bash
   kubectl apply -f nginx-health-checks.yaml
   ```

4. Observe the Pod behavior during startup:
   ```bash
   kubectl get pods --watch
   ```
   **Expected Outcome**: You should see the pod in a 'Starting' state for about 30 seconds before it becomes ready.



### **Step 6: Cleanup**
1. Delete the Pod after completing the lab:
   ```bash
   kubectl delete pod nginx
   ```

## **Submission Guidelines**

1. Make sure all the steps in the lab have been followed.
2. Provide screenshots or terminal outputs showing the results of each task.

Note: The screenshots should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional Resources

- [Health checks configuring in K8s](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)