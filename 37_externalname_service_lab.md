# Kubernetes ExternalName Service with Nginx


## **Overview**:
In this lab, we will explore how to create and use an `ExternalName` service in Kubernetes. An `ExternalName` service allows you to point to an existing service or external resource, like an `nginx` deployment within the Kubernetes cluster, by resolving its DNS name. We will create an Nginx service and use an `ExternalName` service to access it from another pod within the cluster.


## **Prerequisites**:
- Minikube cluster is up and running.
- `kubectl` is configured to interact with your Minikube cluster.
- Basic knowledge of Kubernetes resources (Deployment, Service).


## **Outcome**:
By the end of this lab, you will:
- Deploy an `nginx` service within the Kubernetes cluster.
- Create an `ExternalName` service that resolves to the deployed `nginx` service.
- Verify DNS resolution of the `ExternalName` service and access the `nginx` service from a pod.


## **Description**:
This lab demonstrates how to set up a Kubernetes `ExternalName` service. The `ExternalName` service type helps to access services by DNS name, even if those services exist outside the cluster. In this case, we'll deploy a basic `nginx` service within the Minikube cluster and use an `ExternalName` service to access it by a service name.


## **TASKS**

### **Task 1: Deploy the Nginx Service**
1. **Objective**: Create a simple `nginx` deployment and expose it as a service.
2. **Instructions**: 
   - Create the `nginx` deployment and service configuration in a file named `nginx-deployment.yaml`.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx-deployment
   spec:
     replicas: 1
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
           image: nginx
           ports:
           - containerPort: 80
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: nginx-service
   spec:
     selector:
       app: nginx
     ports:
     - protocol: TCP
       port: 80
       targetPort: 80
     type: ClusterIP

   ```

   - Apply the file to the cluster:
   
   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```

   - Verify the service is running:
   
   ```bash
   kubectl get services
   ```

   You should see the `nginx-service` listed with a `ClusterIP`.



### **Task 2: Create the ExternalName Service**
1. **Objective**: Create a service that maps to the `nginx-service` using an `ExternalName`.
2. **Instructions**:
   - Write the following YAML in a file named `external-name-service.yaml`:

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: external-nginx
   spec:
     type: ExternalName
     externalName: nginx-service.default.svc.cluster.local
   ```

   - Apply the file:

   ```bash
   kubectl apply -f external-name-service.yaml
   ```
   
    - Verify the service is running:
   
   ```bash
   kubectl get services
   ```

   You should see the `external-nginx` listed with a `ExternalName`.



### **Task 3: Test the ExternalName Service**
1. **Objective**: Deploy a test pod, verify DNS resolution, and access the `nginx` service through the `ExternalName` service.
2. **Instructions**:
   - Deploy a simple test pod:

   ```bash
   kubectl run test-pod --image=busybox --restart=Never -- sleep 3600
   ```

   - Access the shell of the test pod:

   ```bash
   kubectl exec -it test-pod -- sh
   ```

   - Test DNS resolution for the `external-nginx` service:

   ```bash
   nslookup external-nginx
   ```

   This should resolve to `nginx-service.default.svc.cluster.local`.

   - Use `wget` to access the `nginx` service via the `ExternalName` service:

   ```bash
   wget -qO- external-nginx
   ```

   You should see the default `nginx` welcome page. Use `exit` command to terminate the shell of test pod.



### **Task 4: Clean Up**
1. **Objective**: Remove the resources created during the lab.
2. **Instructions**:
   - Delete the deployment, services, and test pod:

   ```bash
   kubectl delete deployment nginx-deployment
   kubectl delete service nginx-service
   kubectl delete service external-nginx
   kubectl delete pod test-pod
   ```


## **Submission Guidelines**:
- Ensure all tasks are completed and the `nginx` service is accessible using the `ExternalName` service.
- Share the YAML configuration files (`nginx-deployment.yaml`, `external-name-service.yaml`) and any command outputs as evidence of completion.

Note: The screenshots and file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`


## **Additional Resources**:
1. [Kubernetes Services Documentation](https://kubernetes.io/docs/concepts/services-networking/service/)
2. [ExternalName Service Type](https://kubernetes.io/docs/concepts/services-networking/service/#externalname)
3. [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
4. [Kubernetes DNS Documentation](https://kubernetes.io/docs/concepts/services-networking/dns-pod-service/)
