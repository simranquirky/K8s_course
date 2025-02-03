# ** Pod Lifecycle**

## **Overview**

This lesson dives into Kubernetes' handling of Pods throughout their life. We'll look at each stage, from when a Pod starts to when it ends. Getting to know these steps will help you see how Kubernetes keeps apps running . You'll also learn when you might need to step in to deal with problems or other things that come up.

## **Lesson Outcomes**

By the end of this lesson, you will:

- Get to know the main stages of a Pod's life cycle.
- Find out what goes on in each stage and how Pods move from one to another.
- Spot possible issues in each stage and how Kubernetes tackles them.

## Explanation

## **Pod Lifecycle Phases**

A Pod's lifecycle represents its current state in the cluster. Kubernetes assigns these states to help manage and monitor workloads effectively.

The main phases of a Pod lifecycle are:

1. **Pending**
2. **Running**
3. **Succeeded**
4. **Failed**
5. **Unknown**

![image.png](https://bobcares.com/wp-content/uploads/2022/07/podstates.png)
Source: https://bobcares.com/wp-content/uploads/2022/07/podstates.png

### **1. Pending**

This is the starting phase when a Pod is first created but hasn’t started running its containers yet.

**What Happens in This Phase?**

- Kubernetes tries to schedule the Pod on a suitable node based on resource availability (CPU, memory, etc.).
- The container images required for the Pod are downloaded (or pulled) to the node.

**Challenges in the Pending Phase**:

- Resource shortages might delay scheduling.
- Image pull issues (e.g., incorrect image name or network restrictions).

### **2. Running**

Once Kubernetes successfully schedules a Pod and starts at least one container, the Pod enters the **Running** phase.

**Key Characteristics of the Running Phase**:

- All the containers in the Pod are up and operational.
- The Pod is performing its intended function, such as serving web traffic or processing data.

**Points to Remember**:

- Even in the Running phase, containers inside the Pod may fail temporarily or restart depending on the configuration (e.g., Restart Policies).

### **3. Succeeded**

A Pod transitions to the **Succeeded** phase when all its containers complete their tasks and exit without errors (exit code `0`).

**When Does This Happen?**

- This phase is common for **batch jobs** or **one-time tasks**, such as processing files or running database migrations.

### **4. Failed**

A Pod moves to the **Failed** phase when one or more of its containers exit with an error (non-zero exit code) and will not restart.

**Why Does This Happen?**

- Application-level issues, such as crashes or incorrect configurations.
- Insufficient resources allocated to the Pod.

### **5. Unknown**

The **Unknown** phase indicates that Kubernetes cannot determine the Pod’s state. This usually happens due to network connectivity issues between the control plane and the node where the Pod is running.

## **Pod Lifecycle with Examples**

Let’s break down the Pod lifecycle with a relatable analogy.

### **Example Scenario**:

Imagine you’re placing an order for a package delivery service:

- Awaiting Dispatch: Your order is live, but not yet shipped out. The system is validating whether there's a free delivery person and that the package is ready.
- Running: This is when you sent the package and it started off. It is being actively carried to you.
- Succeed Phase — Package delivered to you.
- Failure Phase : The delivery cancelled, probably due to an invalid address or something.
- Unknown Phase : You stop see the order in between the communication chain between you and your delivery person

Pods in Kubernetes are also managed in similar way by Kubelet - they progress through these phases depending on their status and events. 

## **Pod Lifecycle in Practice**

To better understand the Pod lifecycle, let’s consider an example. Imagine a simple application that processes incoming messages and writes them to a log file.

- **Pending**: The application Pod is being prepared, and the required container image is pulled.
- **Running**: The application Pod starts processing messages and writing logs.
- **Succeeded**: After processing all messages, the application completes its task and exits successfully.
- **Failed**: If the application encounters a fatal error (e.g., invalid configuration or lack of memory), the Pod transitions to the Failed phase.
- **Unknown**: If there’s an issue with the Kubernetes control plane, the Pod status might temporarily be marked as Unknown.


## Pod Lifetime 

Pods and application containers are transient objects. They are assigned a unique identity (UID) upon creation and stay in their designated node until they are deleted or terminated—according to their restart policy. 

Due to their inability to function without the resources or upkeep of the node, pods scheduled to a dead or failed node are removed (after a timeout period). They cannot be rescheduled to a different node, which would need a change in their UID, or they can self-heal. Rather, the controller launches the pod to an eligible node again with a new UID.

Storage volumes and other pod-related entities, like persistent volumes (PV), are frequently associated with a pod if their existence is dependent upon that of that particular pod. All associated entities are erased along with a pod when it is deleted, and new, identical entities are created in its place when a new pod is created.

## Suggested Reading
- [Pods Liefcycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)
