
# Setting Up Azure Kubernetes Service (AKS)

## Lab Overview

In this lab, you will learn how to set up and manage a Kubernetes cluster using **Azure Kubernetes Service (AKS)**. You’ll walk through creating an AKS cluster, connecting to it using `kubectl`, deploying a sample application, and scaling the application.

## Pre-requisites

Before starting this lab, ensure you have the following:

1. **Azure CLI** installed and configured on your machine.
   - You can install the Azure CLI [here](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).
   
2. **kubectl** installed on your machine.
   - Install it by following the official [kubectl installation guide](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
   
3. An **Azure account**. You can create a free Azure account [here](https://azure.microsoft.com/en-us/free/).

4. Basic knowledge of **Kubernetes** concepts (Pods, Deployments, Services).

## Outcomes

By the end of this lab, you will be able to:

- Create an Azure Kubernetes Service (AKS) cluster using the Azure CLI.
- Connect to your AKS cluster using `kubectl`.
- Deploy a sample application to the AKS cluster.
- Expose the application using a LoadBalancer.
- Scale the application to handle more traffic.

## Description

In this lab, you will:

1. **Create an Azure Resource Group** to hold your AKS resources.
2. **Create an AKS Cluster** using the Azure CLI.
3. **Connect to the AKS Cluster** using `kubectl`.
4. **Deploy a sample application** (e.g., Nginx) to the AKS cluster.
5. **Scale the application** to handle more requests.
6. **Expose the application** to the internet via a LoadBalancer.

## TASKS

### Task 1: Set Up Azure Resource Group

1. Open the **Azure CLI** and log in to your Azure account:
   ```bash
   az login
   ```

2. Create a new **Resource Group** to organize the resources for this lab. Choose your preferred location:
   ```bash
   az group create --name aks-resource-group --location eastus
   ```

   This command creates a resource group called `aks-resource-group` in the `eastus` region.

### Task 2: Create an AKS Cluster

1. Now, create an AKS cluster within the resource group you just created. The following command creates a cluster with 3 nodes:
   ```bash
   az aks create \
     --resource-group aks-resource-group \
     --name aks-cluster \
     --node-count 3 \
     --enable-addons monitoring \
     --generate-ssh-keys
   ```

   **Explanation of flags:**
   - `--node-count 3`: Creates 3 nodes in the cluster.
   - `--enable-addons monitoring`: Enables monitoring features in AKS.
   - `--generate-ssh-keys`: Automatically generates SSH keys for access to the nodes.

2. Wait for the command to complete. It may take several minutes to provision the AKS cluster.

### Task 3: Connect to the AKS Cluster

1. Once the cluster is created, configure `kubectl` to connect to the AKS cluster:
   ```bash
   az aks get-credentials --resource-group aks-resource-group --name aks-cluster
   ```

   This command fetches the credentials required to authenticate with the AKS cluster and configures `kubectl` to use them.

2. Verify that `kubectl` is connected to your AKS cluster:
   ```bash
   kubectl get nodes
   ```

   This should list the nodes in your cluster.

### Task 4: Deploy a Sample Application

1. To deploy a sample application, create a Kubernetes Deployment. First, create a YAML file (`nginx-deployment.yaml`) with the following contents:
   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: nginx
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
   ```

2. Apply the deployment to your AKS cluster:
   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```

3. Verify the deployment:
   ```bash
   kubectl get deployments
   ```

   This should show the `nginx` deployment with 2 replicas.

### Task 5: Expose the Application Using a LoadBalancer

1. Create a service to expose the application externally. Create a new YAML file (`nginx-service.yaml`) with the following contents:
   ```yaml
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
     type: LoadBalancer
   ```

2. Apply the service:
   ```bash
   kubectl apply -f nginx-service.yaml
   ```

3. Verify that the service is created and has an external IP address:
   ```bash
   kubectl get svc
   ```

   Wait for a few minutes until the `EXTERNAL-IP` column is populated with an IP address.

4. Access the application using the external IP address provided.

### Task 6: Scale the Application

1. To scale your application, use the `kubectl scale` command:
   ```bash
   kubectl scale deployment nginx --replicas=5
   ```

2. Verify that the deployment is scaled:
   ```bash
   kubectl get deployments
   ```

   This should now show 5 replicas for the `nginx` deployment.

## Submission Guidelines

1. Ensure that all commands are executed successfully and output is captured.
2. Provide the final IP address of the exposed service.
3. Include a screenshot of the `kubectl get nodes`, `kubectl get deployments`, and `kubectl get svc` commands showing the status of your cluster and deployed application.

Note: The screenshots and the file content should be added to a google doc or google drive the link to which should be shared with permissions set as `accessible to all`

## Additional resources

- [Getting started with AKS](https://learn.microsoft.com/en-us/azure/aks/what-is-aks#get-started-with-aks)