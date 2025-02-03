# Working with Local Persistent Volumes in Kubernetes

## Lab Overview

This lab demonstrates how to create and manage **Local Persistent Volumes (PVs)** in Kubernetes, provision a **PersistentVolumeClaim (PVC)**, and use it within a **Pod** to store data. You will also explore the persistence of data in a local volume when a Pod is deleted and recreated using a **Deployment**.

## Pre-requisites

- **Minikube** installed and running with Docker as the driver.
- **kubectl** installed and configured to work with your Minikube cluster.
- Basic understanding of Kubernetes concepts such as Pods, Persistent Volumes, and PersistentVolumeClaims.
- Familiarity with YAML configuration files.

## Outcomes

By the end of this lab, you will:
- Learn how to create a **PersistentVolume** using local storage in Minikube.
- Provision a **PersistentVolumeClaim (PVC)** that requests storage from the PersistentVolume.
- Use a **Pod** to store data on the local volume.
- Understand how data persists even when Pods are deleted and recreated by using a **Deployment**.

## Description

In this lab, you will use Minikube to create a **PersistentVolume** backed by a local storage device on the Minikube VM. You will then create a **PersistentVolumeClaim** (PVC) to request storage from the PV, and use a **Pod** to store data on the local volume. You will also test data persistence by deleting and recreating the Pod through a **Deployment**.

The steps will guide you through setting up the local volume, provisioning storage with PVCs, and ensuring that data persists even when a Pod is deleted.

## TASKS

### Task 1: Set Up Local Storage in Minikube VM
1. Open a terminal and run the following command into the Minikube VM:  
   ```bash
   docker ps
   docker exec -it minikube /bin/bash 
   ```  
2. Create a directory for local storage:
   ```bash
   sudo mkdir -p /mnt/data
   ```
3. Exit the Minikube VM:
   ```bash
   exit
   ```

### Task 2: Create the PersistentVolume (PV)
1. Create a file `local-pv.yaml` with the following content:
   ```yaml
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: local-pv
   spec:
     capacity:
       storage: 5Gi
     volumeMode: Filesystem
     accessModes:
       - ReadWriteOnce
     persistentVolumeReclaimPolicy: Retain
     storageClassName: manual
     local:
       path: /mnt/data
     nodeAffinity:
       required:
         nodeSelectorTerms:
           - matchExpressions:
               - key: kubernetes.io/hostname
                 operator: In
                 values:
                   - minikube
   ```
2. Apply the PersistentVolume configuration:
   ```bash
   kubectl apply -f local-pv.yaml
   ```

### Task 3: Create the PersistentVolumeClaim (PVC)
1. Create a file `local-pvc.yaml` with the following content:
   ```yaml
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: local-pvc
   spec:
     accessModes:
       - ReadWriteOnce
     storageClassName: manual
     resources:
       requests:
         storage: 5Gi
   ```
2. Apply the PVC configuration:
   ```bash
   kubectl apply -f local-pvc.yaml
   ```

### Task 4: Verify the PV and PVC
1. Verify the PersistentVolume and PersistentVolumeClaim:
   ```bash
   kubectl get pv
   kubectl get pvc
   ```

### Task 5: Create a Deployment to Use the PVC
1. Create a file `local-deployment.yaml` with the following content:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: local-deployment
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: local-app
     template:
       metadata:
         labels:
           app: local-app
       spec:
         containers:
           - name: nginx
             image: nginx
             volumeMounts:
               - mountPath: /usr/share/nginx/html
                 name: local-storage
         volumes:
           - name: local-storage
             persistentVolumeClaim:
               claimName: local-pvc
   ```
2. Apply the Deployment configuration:
   ```bash
   kubectl apply -f local-deployment.yaml
   ```

### Task 6: Test Data Persistence
1. Exec into the running Pod and create a test file in the mounted volume:
   ```bash
   kubectl exec -it <pod-name> -- /bin/bash
   echo "Hello from the local volume" > /usr/share/nginx/html/index.html
   exit
   ```
2. Delete the Pod managed by the Deployment:
   ```bash
   kubectl delete pod -l app=local-app
   ```
3. Verify that the Pod is recreated and the data persists:
   ```bash
   kubectl get pods -w
   kubectl exec -it <new-pod-name> -- cat /usr/share/nginx/html/index.html
   ```

### Task 7: Clean Up Resources
1. Delete the Deployment, PVC, and PV:
   ```bash
   kubectl delete deployment local-deployment
   kubectl delete pvc local-pvc
   kubectl delete pv local-pv
   ```

## Submission Guidelines

- Submit your lab files (YAML files) and any relevant screenshots or logs showing the successful creation of the PersistentVolume, PVC, Deployment, and verification of data persistence.

Note: The screenshots and the file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`


## Additional Resources

- [Kubernetes Persistent Volumes Documentation](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
- [Kubernetes Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
