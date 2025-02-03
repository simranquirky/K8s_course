
# **The `kubectl` Commands**

## **Overview**

In this lesson, we’ll introduce `kubectl`, the command-line tool for interacting with Kubernetes. We’ll start by understanding why `kubectl` is essential, what it does, and then explore some basic commands to interact with your Kubernetes cluster.

## **Lesson Outcomes**

By the end of this lesson, you will:

- Understand the purpose of `kubectl` and why it is essential for managing Kubernetes.
- Learn what `kubectl` is and how it acts as a bridge between you and Kubernetes.
- Get familiar with commonly used `kubectl` commands for managing Pods and clusters.

## Explanation

Kubectl is the command-line tool for interacting with Kubernetes clusters. It serves as the primary interface for administrators, developers, and users to manage applications and resources within a Kubernetes cluster.

### **Why Do We Need `kubectl`?**

Managing Kubernetes without `kubectl` is like navigating a complex city without a map or GPS. While Kubernetes is powerful, interacting with it directly is not user-friendly. That’s where `kubectl` comes in:

1. **Communication Bridge**: It lets you communicate with the **Kubernetes API server**, translating your commands into actions Kubernetes can execute.
2. **Simplified Resource Management**: Instead of writing complex API calls, you can use simple commands to create, inspect, and manage resources like Pods, Services, and Deployments.
3. **Real-Time Insights**: From checking the status of your cluster to viewing logs and events, `kubectl` helps you monitor and debug easily.

In short, `kubectl` makes Kubernetes accessible and manageable.

### **What is `kubectl`?**

Kubectl is the command-line tool for interacting with Kubernetes clusters. It serves as the primary interface for administrators, developers, and users to manage applications and resources within a Kubernetes cluster.

Here's a breakdown of its key functions and utilities:

- **Resource Management:** kubectl allows users to create, inspect, update, and delete various Kubernetes resources such as pods, deployments, services, replica sets, namespaces, secrets, configmaps, and more. These resources are defined in YAML or JSON format and can be managed using kubectl commands.

- **Cluster Interaction:** Users can interact with Kubernetes clusters using kubectl commands to view cluster information, manage contexts, switch between clusters, and set configurations. It provides capabilities for cluster-wide operations, including listing nodes, viewing cluster information, and managing access controls.

- **Control and Monitoring:** kubectl offers commands to control and monitor the state of Kubernetes resources. Users can inspect the status of pods, deployments, and other resources, monitor resource usage, view logs, check events, and troubleshoot issues within the cluster.

- **Deployment Management:** Users can use kubectl to manage deployments, including rolling out updates, scaling applications, rolling back changes, and managing deployment history. kubectl facilitates deployment strategies such as rolling updates, blue-green deployments, and canary releases.

- **Namespace Management:** Kubernetes uses namespaces to organize and isolate resources within a cluster. With kubectl, users can create, list, and delete namespaces, as well as view resources within specific namespaces. Namespaces provide a way to partition resources and manage multi-tenancy within a cluster.

- **Secrets and ConfigMaps:** kubectl provides commands to manage secrets and configmaps, which are used to store sensitive information and configuration data, respectively. Users can create, update, and delete secrets and configmaps, as well as mount them into pods as volumes or environment variables.

- **Debugging and Troubleshooting:** kubectl offers commands for debugging and troubleshooting Kubernetes applications and resources. Users can view pod logs, execute commands within pods, perform port forwarding, copy files to and from pods, and inspect resource configurations for errors or misconfiguration.

## Commonly used kubetcl commands.

- `kubectl create`: This command is used to create various Kubernetes resources such as pods, services, deployments, etc.
---
- `kubectl apply`: This command is similar to kubectl create, but it can create or update resources based on YAML or JSON files.
---
- `kubectl get`: This command is used to retrieve information about Kubernetes resources.
    - For example, `kubectl get pods` will list all pods in the current namespace.
---
- `kubectl describe`: This command provides detailed information about a specific Kubernetes resource.
    - For example, `kubectl describes pod` will give detailed information about the specified pod.
---
- `kubectl delete`: This command is used to delete Kubernetes resources.
    - For example, `kubectl delete pod` will delete the specified pod.
---
- `kubectl logs`: This command is used to view the logs of a specific pod.
    - For example, `kubectl logs` will display the logs of the specified pod.
---
- `kubectl exec`: This command is used to execute commands inside a running container of a pod.
    - For example, `kubectl exec -it -- /bin/bash` will open an interactive shell inside the specified pod.
---
- `kubectl rollout`: This command is used to manage rollouts of deployments.
    - For example, `kubectl rollout status deployment` will show the status of the rollout for the specified deployment.
---
- `kubectl scale`: This command is used to scale the number of replicas of a deployment, replica set, or replication controller.
    - For example, `kubectl scale deployment --replicas=3` will scale the specified deployment to have three replicas.
---
- `kubectl port-forward`: This command is used to forward one or more local ports to a pod.
    - For example, `kubectl port-forward 8080:80` will forward port 8080 on the local machine to port 80 on the specified pod.
---
- `kubectl edit`: This command opens the specified resource in the default text editor, allowing you to edit its configuration.
    - For example, `kubectl edit pod` will open the specified pod's configuration in the default editor.
---
- `kubectl rollout restart`: This command restarts the rollout of a deployment, effectively redeploying the application.
    - For example, `kubectl rollout restart deployment` will restart the rollout for the specified deployment.
---
- `kubectl create secret`: This command is used to create a secret. Secrets are used to store sensitive information such as passwords, OAuth tokens, and SSH keys.     - For example, `kubectl creates a secret generic --from-literal==` creates a generic secret from a literal value.
---
- `kubectl get events`: This command displays events related to Kubernetes resources. It can be useful for troubleshooting and monitoring.
    - For example, `kubectl get events --sort-by=.metadata.creationTimestamp` will display events sorted by creation timestamp.
---
- `kubectl label`: This command is used to add or update labels on Kubernetes resources. Labels are key-value pairs used to organize and select resources.
    - For example, `kubectl label pods app=backend` adds the label app=backend to the specified pod.
---
- `kubectl exec -it`: This command was mentioned earlier for executing commands inside a running container. The -it flag opens an interactive terminal for executing multiple commands.
---
- `kubectl rollout history`: This command shows the rollout history of a deployment. It displays revisions of the deployment and their status.
    - For example, `kubectl rollout history deployment` will show the rollout history of the specified deployment.
---
- `kubectl top`: This command is used to view resource usage statistics for Kubernetes objects such as nodes and pods.
    - For example, `kubectl top pods` will display CPU and memory usage for all pods in the current namespace.
---
- `kubectl cp`: This command copies files and directories to and from Kubernetes pods.
    - For example, `kubectl cp:/path/to/remote/file /path/to/local/file` copies a file from the specified pod to the local file system.
---
- `kubectl version`: This command displays the client and server versions of kubectl and the Kubernetes cluster. It can be useful for verifying compatibility between client and server versions.

Don't worry you don't need to remember them all, we will be making use of them in further labs and lessons.

## Suggested Reading
- [Kubectl- command line tool](https://kubernetes.io/docs/reference/kubectl/)