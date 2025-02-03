# **Using hostPath Volume in Kubernetes**  


## **Lab Overview**  
In this lab, you will learn how to create and use a `hostPath` volume in Kubernetes. You will mount a file or directory from the Minikube VM into a Pod and verify the functionality of the mounted volume. This exercise demonstrates how Kubernetes enables containerized applications to access files from the host system.  



## **Pre-requisites**  
- **Minikube** installed and running on your system.  
- Basic understanding of Kubernetes Pods and YAML manifests.  
- Familiarity with Minikube commands.  
- A system with **Docker** (Minikube running in Docker).  



## **Outcomes**  
By the end of this lab, you will:  
1. Understand how to use `hostPath` volumes to share data between the host and a Pod.  
2. Deploy a Kubernetes Pod that uses a `hostPath` volume.  
3. Verify the correct mounting of files or directories into the container.  



## **Description**  
In this lab, you will:  
1. Access the Minikube VM to create a directory that serves as the host path.  
2. Write a Kubernetes manifest to mount the directory inside a Pod.  
3. Deploy the Pod and validate the setup by verifying files shared between the Minikube VM and the Pod.  

This lab focuses on scenarios where you might want to share configuration files, logs, or other persistent data between a containerized application and its host environment.  



## **TASKS**  

### **Task 1: Connect with Minikube VM**  
1. Open a terminal and run the following command into the Minikube VM:  
   ```bash
   docker ps
   docker exec -it minikube /bin/bash 
   ```  

2. Create a directory in the Minikube VM to be used as the host path:  
   ```bash  
   mkdir /mnt/data  
   echo "Hello from Minikube VM!" > /mnt/data/hello.txt  
   ```  



### **Task 2: Create a Kubernetes Manifest**  
1. Write a YAML file for a Kubernetes Pod (e.g., `hostpath-pod.yaml`) with a `hostPath` volume.  
2. Use the following example manifest:  
   ```yaml  
   apiVersion: v1  
   kind: Pod  
   metadata:  
     name: hostpath-pod  
   spec:  
     containers:  
     - name: test-container  
       image: nginx  
       volumeMounts:  
       - mountPath: /usr/share/nginx/html  
         name: test-volume  
     volumes:  
     - name: test-volume  
       hostPath:  
         path: /mnt/data  
         type: DirectoryOrCreate  
   ```  



### **Task 3: Deploy the Pod**  
1. Apply the YAML manifest using `kubectl`:  
   ```bash  
   kubectl apply -f hostpath-pod.yaml  
   ```  

2. Confirm that the Pod is running:  
   ```bash  
   kubectl get pods  
   ```  



### **Task 4: Verify the hostPath Volume**  
1. Access the Pod:  
   ```bash  
   kubectl exec -it hostpath-pod -- ls /usr/share/nginx/html  
   ```  

2. Check the contents of the file from the mounted volume:  
   ```bash  
   kubectl exec -it hostpath-pod -- cat /usr/share/nginx/html/hello.txt  
   ```  

3. Add more files in the Minikube VM:  
   ```bash  
   echo "Another file!" > /mnt/data/another.txt  
   ```  

4. Verify the new file inside the Pod:  
   ```bash  
   kubectl exec -it hostpath-pod -- ls /usr/share/nginx/html  
   kubectl exec -it hostpath-pod -- cat /usr/share/nginx/html/another.txt  
   ```

### **Task 5: Clean Up**
1. Delete the directory on Minikube VM:

   ```bash
   rm -rf mnt/data
   ```
   
2. Delete the hostpath-pod:

   ```bash
   kubectl delete pod hostpath-pod
   ```


## **Submission Guidelines**  
Submit the following evidence:  
   - Screenshot of the YAML manifest file.  
   - Output of the `kubectl get pods` command.  
   - Output of the `kubectl exec` commands showing the file contents inside the container.  


Note: The screenshots and the file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## **Additional Resources**  
- [Kubernetes Documentation: hostPath Volumes](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath)  
- [Minikube Official Documentation](https://minikube.sigs.k8s.io/docs/)  
- [Kubernetes CLI Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)  


