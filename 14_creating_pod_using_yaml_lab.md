
# Creating and Managing Pods Using YAML  

## **Lab Overview**  

In this lab, you will learn how to create and manage Kubernetes Pods using YAML files. This includes writing a YAML file, applying it to create a Pod, verifying the Pod's status, and performing basic operations like inspecting and deleting the Pod.  


## **Pre-requisites**  

1. A functional Kubernetes cluster (Minikube, Kind, or a managed Kubernetes cluster).  
2. kubectl installed and configured to access the cluster.  
3. Basic understanding of what a Pod is and its lifecycle.  

## **Outcomes**  

By the end of this lab, you will:  

- Understand how to define a Pod in YAML.  
- Use the `kubectl` commands to create, inspect, and delete Pods using YAML files.  
- Learn to verify and troubleshoot Pod statuses.  

## **Description**  

In this guided lab, you will:  

1. Write a simple YAML file defining a Pod running an Nginx container.  
2. Apply the YAML file to create the Pod.  
3. Inspect the Pod's status and logs.  
4. Delete the Pod when it's no longer needed.  

Each step includes detailed explanations of the commands and their purpose.  

## **TASKS**  

### **Task 1: Writing the YAML File**  

1. Open a terminal and create a YAML file named `nginx-pod.yaml`:
   ```bash
   notepad nginx-pod.yaml
   ```
2. Add the following content to define a Pod:
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: nginx-pod
     labels:
       app: nginx
   spec:
     containers:
     - name: nginx-container
       image: nginx:latest
       ports:
       - containerPort: 80
   ```
   **Explanation**:  
   - `apiVersion`: Specifies the Kubernetes API version.  
   - `kind`: Defines the resource type (`Pod`).  
   - `metadata`: Provides metadata like the Pod name and labels.  
   - `spec`: Contains the desired configuration for the Pod.  
   - `containers`: Lists the containers in the Pod, including the image to use (`nginx:latest`) and the exposed port (80).  

3. Save and exit the file.  


### **Task 2: Creating the Pod**  

1. Use the following command to create the Pod using your YAML file:
   ```bash
   kubectl apply -f nginx-pod.yaml
   ```
   **What This Does**:  
   - The `apply` command tells Kubernetes to create or update resources based on the YAML file.  
   - `-f` specifies the file path.  

2. Verify that the Pod was created:
   ```bash
   kubectl get pods
   ```
   **Explanation**:  
   - This command lists all Pods in the current namespace, displaying their name, status, and age.  


### **Task 3: Inspecting the Pod**  

1. Describe the Pod to view detailed information:
   ```bash
   kubectl describe pod nginx-pod
   ```
   **What This Does**:  
   - Shows events, container details, resource requests/limits, and any errors.  
   - Use this command to troubleshoot Pods that fail to start.  

2. Check the Pod logs:
   ```bash
   kubectl logs nginx-pod
   ```
   **What This Does**:  
   - Displays the logs for the container running inside the Pod.  
   - Useful for debugging issues with applications running in the Pod.  

### **Task 4: Testing Pod Connectivity**  

1. Start a temporary shell in the Pod:
   ```bash
   kubectl exec -it nginx-pod -- /bin/sh
   ```
   **What This Does**:  
   - `exec` runs a command in a running container inside the Pod.  
   - `-it` enables interactive mode to access the shell.  

2. Test the web server by curling `localhost` from inside the Pod:
   ```bash
   curl localhost
   ```
   **Expected Output**: You should see the default Nginx welcome page HTML.  

3. Exit the shell:
   ```bash
   exit
   ```

### **Task 5: Deleting the Pod**  

1. Delete the Pod when you're done:
   ```bash
   kubectl delete pod nginx-pod
   ```
   **What This Does**:  
   - Removes the Pod and frees up any resources it used.  

2. Verify deletion:
   ```bash
   kubectl get pods
   ```
   **Expected Output**: The Pod `nginx-pod` should no longer appear in the list.  


## **Submission Guidelines**  

1. Submit the `nginx-pod.yaml` file you created.  
2. Provide screenshots showing:  
   - Pod creation (`kubectl get pods`).  
   - Pod description (`kubectl describe pod nginx-pod`).  
   - Logs (`kubectl logs nginx-pod`).  

Note: The screenshots and file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## **Additional Resources**  

- [Kubernetes Documentation: Pods](https://kubernetes.io/docs/concepts/workloads/pods/)  
- [kubectl Command Reference](https://kubernetes.io/docs/reference/kubectl/)  
- [Learn YAML Basics](https://yaml.org)  

