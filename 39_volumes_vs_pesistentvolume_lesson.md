# Volumes vs Persistent Volumes in Kubernetes  

## **Lesson Overview**  
In this lesson, we will compare Kubernetes Volumes and PersistentVolumes, highlighting their differences, use cases, and how they work in containerized applications. By understanding this distinction, you’ll be better equipped to choose the right storage solution for your Kubernetes workloads.

## **Learning Outcomes**  
By the end of this lesson, you will:  
1. Understand the difference between Volumes and PersistentVolumes.  
2. Learn the use cases for Volumes and PersistentVolumes.  
3. Explore how these storage mechanisms work within Kubernetes.  

## Explanation
### **Understanding Volumes in Kubernetes**  

#### **1. What Are Volumes?**  
- Volumes are a storage abstraction that allows pods to access data outside their ephemeral container filesystem.  
- They are created and managed at the **pod level**.  
- Lifecycle: Tied to the lifecycle of the pod. Once the pod is deleted, the volume and its data are also removed (unless it’s a shared external storage).  

**Common Volume Types**:  
1. **emptyDir**: Temporary storage that lasts for the lifetime of a pod.  
2. **hostPath**: Directly maps files or directories on the node’s filesystem.  
3. **ConfigMap/Secret**: Injects configuration data or sensitive information.  
4. **Cloud-Specific Volumes**: e.g., `awsElasticBlockStore`, `azureDisk`, `gcePersistentDisk`.  

#### **When to Use Volumes?**  
- Temporary data storage needed only while the pod is running.  
- Sharing data between containers within the same pod.  
- Accessing node-local data.  


### **What Are PersistentVolumes (PVs)?**  
Kubernetes supports Persistent Volumes. With Persistent Volumes, data is persisted regardless of the lifecycle of the application, container, Pod, Node, or even the cluster itself.

A Persistent Volume (PV) object represents a storage volume that is used to persist application data. A PV has its own lifecycle, separate from the lifecycle of Kubernetes Pods.

A PV essentially consists of two different things:

- A backend technology called a PersistentVolume
- An access mode tells Kubernetes how the volume should be mounted.

A PV is an abstract component, and the actual physical storage must come from somewhere.

Here are a few examples:

- csi: Container Storage Interface (CSI) → (for example, Amazon EFS, Amazon EBS, Amazon FSx, etc.)
- iscsi: iSCSI (SCSI over IP) storage
- local: Local storage devices mounted on nodes
- nfs: Network File System (NFS) storage

### Access mode

The access mode is set during PV creation and tells Kubernetes how the volume should be mounted. Persistent Volumes support three access modes:

- ReadWriteOnce: Volume allows read/write by only one node at the same time.
- ReadOnlyMany: Volume allows read-only mode by many nodes at the same time.
- ReadWriteMany: Volume allows read/write by multiple nodes at the same time.

#### **1. Key Features of PersistentVolumes**  
- A **PersistentVolume** (PV) is a cluster-level resource that provides **independent, long-term storage** for pods.  
- PVs are not tied to the lifecycle of a specific pod. This means data persists even if a pod is deleted.  
- PVs abstract the underlying storage infrastructure, allowing for portability across cloud providers or on-premises environments.

#### **2. How PersistentVolumes Work**  
PersistentVolumes are part of Kubernetes’ storage system and follow a **two-step binding process**:  
1. **Provisioning**:  
   - A PersistentVolume is created, either manually or dynamically.  
   - Storage can come from local disks, cloud storage, or networked file systems.  
2. **Claiming**:  
   - Pods don’t directly interact with PVs. Instead, they request storage through a **PersistentVolumeClaim (PVC)**.  
   - The PVC specifies the required storage size, access mode, and other parameters. Kubernetes binds the PVC to a matching PV.  

#### **Types of PersistentVolumes**  
- **Static Provisioning**: Administrator manually creates the PV.  
- **Dynamic Provisioning**: Kubernetes dynamically provisions a PV based on PVC requests and StorageClass configurations.  

### **Key Differences: Volumes vs PersistentVolumes**

| Feature                | Volume                                  | PersistentVolume (PV)                    |
|------------------------|-----------------------------------------|------------------------------------------|
| **Scope**              | Pod-specific                           | Cluster-level                            |
| **Lifecycle**          | Tied to the pod                        | Independent of the pod                   |
| **Persistence**        | Temporary, data lost after pod deletion| Long-term, data persists after pod deletion |
| **Provisioning**       | Defined in pod specification           | Managed at the cluster level (manually or dynamically) |
| **Use Cases**          | Temporary data, scratch space          | Persistent storage for databases, logs, etc. |
 

### **When to Use Volumes vs PersistentVolumes?**  
- **Use Volumes** when:  
  - The data is only needed temporarily during the lifecycle of a pod.  
  - The application is stateless.  

- **Use PersistentVolumes** when:  
  - Data must persist beyond the pod’s lifecycle.  
  - Applications are stateful or require shared storage.  

## Persistent Volume Claims

A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a Pod.
Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., they can be mounted ReadWriteOnce, ReadOnlyMany, ReadWriteMany, or ReadWriteOncePod).

PVs are resources in the cluster. PVCs are requests for those resources and also act as claim checks to the resource.The separation between PV and PVC relates to the idea that there are two types of people in a Kubernetes environment:

- Kubernetes administrator: this person is supposed to maintain the cluster, operate it, and add computational resources such as persistent storage.
- Kubernetes application developer: this person is supposed to develop and deploy the application.

## Suggested Reading
- [Persistent Volumes in K8s - documentation](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)