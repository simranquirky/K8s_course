# **Project Title: Django Notes App on Minikube (Windows Environment)**

## **Project Overview**

This project aims to set up a simple **Django Notes application** on a local **Kubernetes cluster** running on **Windows** using **Minikube**. The goal is to demonstrate the process of containerizing a Django application, deploying it on Kubernetes, and exposing it through a service. The project will involve integrating key Kubernetes concepts like **Deployments** and **Services** while running everything in a **Minikube** environment, which simulates a production-like setup locally.

### **End Goal**

The end goal is to successfully deploy a Django-based Notes application on a **Kubernetes cluster** running on Windows. The application will expose REST APIs to manage notes, providing a basic CRUD functionality. The project will also involve exploring how to manage application deployment and service exposure in Kubernetes. Ultimately, you'll have a local, isolated environment that mimics real-world Kubernetes infrastructure.

## **Pre-requisites**

1. **Windows 10/11 (Pro or Enterprise)**
2. **Virtualization support enabled** in BIOS
3. **Docker Desktop for Windows** (with **WSL 2** integration)
4. **Minikube** installed on Windows
5. **kubectl** for interacting with Kubernetes clusters
6. Basic knowledge of **Docker**, **Kubernetes**, and **Django** (optional)

## **Outcomes**

By the end of the project, you will:

- Set up **Minikube** on a Windows machine and configure **kubectl**.
- Deploy a **Django-based Notes application** to a Kubernetes cluster.
- Expose the Django application using a **Kubernetes Service**.
- Gain a deeper understanding of **Kubernetes** concepts such as Deployments and Services.

## **Project Description**

This project involves running a simple **Django Notes Application** within a local **Kubernetes** environment set up using **Minikube**. The application will provide basic functionality to create, read, update, and delete notes through a REST API. The project will demonstrate how to manage application deployment and expose it via a service.

### **Application Architecture**

1. **Frontend:**
   - Django framework to create a REST API for managing notes.
   - Exposes CRUD endpoints for notes.
   
2. **Backend:**
   - Containerized using **Docker**.

3. **Kubernetes:**
   - **Minikube** for running the Kubernetes cluster on Windows.
   - **Deployment** to ensure high availability with multiple replicas.
   - **Service** to expose the Django application to external traffic.

---

## **TASKS**

### **1. Install Pre-requisites**

#### **1.1 Install Docker Desktop for Windows**
- Download and install **Docker Desktop for Windows** with **WSL 2** integration.
- Verify the installation using the command:
  
```bash
docker --version
```

#### **1.2 Install Minikube**
- Download and install **Minikube** using **choco** or from the Minikube website.
- Start Minikube using the Docker driver:

```bash
minikube start --driver=docker
```

#### **1.3 Install kubectl**
- Install **kubectl** either via **choco** or manually.
- Verify the installation:

```bash
kubectl version --client
```

---

### **2. Set Up Kubernetes Cluster**

#### **2.1 Start Minikube**
- Start the Minikube cluster using the Docker driver.

```bash
minikube start --driver=docker
```

- Check the status of the Minikube cluster:

```bash
minikube status
kubectl get nodes
```

#### **2.2 Create Kubernetes Namespace**
- Create a namespace for better isolation of resources.

**namespace.yml**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: notes-app
```

```bash
kubectl apply -f namespace.yml
kubectl get ns
```

---

### **3. Deploy Django Notes Application**

#### **3.1 Create Deployment**
- Define a deployment to run the Django Notes app.

**deployment.yml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: notes-app-deployment
  namespace: notes-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: notes-app
  template:
    metadata:
      labels:
        app: notes-app
    spec:
      containers:
      - name: notes-app
        image: simkum123/note-app:latest
        ports:
        - containerPort: 8000
```

Apply the deployment:

```bash
kubectl apply -f deployment.yml
kubectl get deploy -n notes-app
```

#### **3.2 Create Service**
- Expose the Django app via a service to allow external access.

**service.yml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: notes-app-service
  namespace: notes-app
spec:
  selector:
    app: notes-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8000
```

Apply the service configuration:

```bash
kubectl apply -f service.yml
```

#### **3.3 Test the Deployment via Port Forwarding**
- Use port forwarding to access the app locally:

```bash
kubectl port-forward service/notes-app-service 8000:80 --address=0.0.0.0 -n notes-app
```

Access the application at `http://localhost:8000`.

