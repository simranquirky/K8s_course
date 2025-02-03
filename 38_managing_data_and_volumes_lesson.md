# Managing Data and Volumes in Kubernetes  


## **Lesson Overview**  
In this lesson, you will learn about the role of volumes in Kubernetes and how they are used to manage data across container lifecycles. We'll cover why volumes are essential, the different types of volumes available, and how to persist application data.


## **Learning Outcomes**  
By the end of this lesson, you will:  
1. Understand why volumes are needed in Kubernetes.  
2. Learn the key types of Kubernetes volumes.  

## Explanation
### **The Need for Volumes in Kubernetes**  

Containers are designed to be ephemeral and stateless. Ephemeral means they're designed to be short-lived, and if they fail, you replace them with new ones instead of fixing them.

Stateless means they were never designed to store data. In fact, if a container fails, all data inside it is lost.

With this in mind, containers should store data in external systems. This is a very simple model in which application code runs in containers and application data is stored outside of them.

A simple cloud example running on AWS might have business application code running inside containers that store the data they generate in AWS elastic block store (EBS) volumes.

This way, if any of the application containers fail, the data still exists in the EBS volumes.

This model decouples the lifecycle of data from the lifecycle of containers and allows you to pick and choose the right storage backend for each containerised application.

![image](https://uptut.gitbook.io/~gitbook/image?url=https%3A%2F%2Fcontent.gitbook.com%2Fcontent%2FzEgYKEnqX736KNXc0NhF%2Fblobs%2FJQrkh2SuKPkUKkN3amiU%2FStorage%2520in%2520k8s.png&width=400&dpr=2&quality=100&sign=794024cd&sv=2)

Kubernetes supports many types of volumes. A Pod can use any number of volume types simultaneously. Ephemeral volume types have a lifetime of a pod, but persistent volumes exist beyond the lifetime of a pod.

When a pod ceases to exist, Kubernetes destroys ephemeral volumes; however, It does not destroy persistent volumes. Data is preserved across container restarts for any kind of volume in a given pod.

## **2. Types of Volumes in Kubernetes**  
Kubernetes supports various volume types to handle different storage requirements.  

![types of volumes](https://uptut.gitbook.io/~gitbook/image?url=https%3A%2F%2Fcontent.gitbook.com%2Fcontent%2FzEgYKEnqX736KNXc0NhF%2Fblobs%2FZKzG4CIQaXPvWIQ6vaX9%2FEmpheral%2520volume.png&width=400&dpr=2&quality=100&sign=5c1e12f9&sv=2)

Kubernetes supports many types of volumes. Some commonly used volumes are:

- emptyDir
- hostPath
- local
- configMap

### emptyDir

For a Pod that defines an emptyDir volume, the volume is created when the Pod is assigned to a node. As the name says, the emptyDir volume is initially empty.

All containers in the Pod can read and write the same files to the emptyDir volume, though each container can mount the volume at the same or different paths.

When a Pod is removed from a node for any reason, the data in the emptyDir is deleted permanently.

emptyDir Configuration example
```
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: saurabhd2106/sample-node-app
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir:
      sizeLimit: 500Mi
```
Use Cases:

- scratch space, such as for a disk-based merge sort
- checkpointing a long computation for recovery from crashes
- holding files that a content-manager container fetches while a webserver container serves the data

### hostPath

A hostPath volume mounts a file or directory from the host node's filesystem into your Pod.

Warning:
Using the hostPath volume type presents many security risks. If you can avoid using a hostPath volume, you should. For example, define a local PersistentVolume and use that instead.

Sample Manifest File for hostPath

```
# This manifest mounts /data/foo on the host as /foo inside the
# single container that runs within the hostpath-example-linux Pod.
#
# The mount into the container is read-only.
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-example-linux
spec:
  os: { name: linux }
  nodeSelector:
    kubernetes.io/os: linux
  containers:
  - name: example-container
    image: registry.k8s.io/test-webserver
    volumeMounts:
    - mountPath: /foo
      name: example-volume
      readOnly: true
  volumes:
  - name: example-volume
    # mount /data/foo, but only if that directory already exists
    hostPath:
      path: /data/foo # directory location on host
      type: Directory # this field is optional
```
### Local

A local volume represents a mounted local storage device such as a disk, partition or directory.

Local volumes can only be used as a statically created persistent volume. Dynamic provisioning is not supported.

Compared to hostPath volumes, local volumes are used in a durable and portable manner without manually scheduling pods to nodes. The system is aware of the volume's node constraints by looking at the node affinity on the PersistentVolume.

However, local volumes are subject to the availability of the underlying node and are not suitable for all applications. If a node becomes unhealthy, then the local volume becomes inaccessible by the pod, and the pod using this volume cannot run. Applications using local volumes must be able to tolerate this reduced availability, as well as potential data loss, depending on the durability characteristics of the underlying disk.

```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: example-pv
spec:
  capacity:
    storage: 100Gi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Delete
  storageClassName: local-storage
  local:
    path: /mnt/disks/ssd1
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - example-node
```

### Config Map

A ConfigMap provides a way to inject configuration data into pods. The data stored in a ConfigMap can be referenced in a volume of type configMap and then consumed by containerized applications running in a pod.

When referencing a ConfigMap, you provide the name of the ConfigMap in the volume. You can customize the path to use for a specific entry in the ConfigMap. The following configuration shows how to mount the log-config ConfigMap onto a Pod called configmap-pod:

```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-pod
spec:
  containers:
    - name: test
      image: busybox:1.28
      command: ['sh', '-c', 'echo "The app is running!" && tail -f /dev/null']
      volumeMounts:
        - name: config-vol
          mountPath: /etc/config
  volumes:
    - name: config-vol
      configMap:
        name: log-config
        items:
          - key: log_level
            path: log_level
```
The log-config ConfigMap is mounted as a volume, and all contents stored in its log_level entry are mounted into the Pod at path /etc/config/log_level. Note that this path is derived from the volume's mountPath and the path keyed with log_level.

NOTE

- You must create a ConfigMap before you can use it.
- A ConfigMap is always mounted as readOnly.
- A container using a ConfigMap as a subPath volume mount will not receive ConfigMap updates.
- Text data is exposed as files using the UTF-8 character encoding. For other character encodings, use binaryData.


## Suggested Reading
- [Volumes in K8s - documentation](https://kubernetes.io/docs/concepts/storage/volumes/)