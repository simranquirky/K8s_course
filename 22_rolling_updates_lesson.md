
# **Rolling Updates and Strategies in Kubernetes**

## **Overview**

In Kubernetes updating apps should go smoothly and the first thing that should be done is ensuring the continuity of apps throughout the update process. Rolling Updates is a deployment strategy that Kubernetes uses to gradually update application instances (Pods) without causing downtime. In this lesson, you will learn about the rolling update process, why it is crucial, and the various options for updating the application with the least impact on the end users.

## **Lesson Outcomes**

By the end of this lesson, you hould have:

- Basic understanding of **Rolling Updates** in Kubernetes.
- Known the principles and approaches for handling updates in a Kubernetes Deployment.
- Be aware of the ways to conduct updates without minimizing the application's availability.
- Been familiar with the configuration and monitoring techniques of **Rolling Updates**.

## **Explanation**

### **Why Are Rolling Updates Important?**

The most essential practice in Kubernetes is to make sure that applications will always be available even during the update process. A traditional application deployment might shut down the application for the update, leading to interruptions in service. However, Kubernetes solves it using **Rolling Updates**.

#### **Benefits of Rolling Updates:**
1. **Zero Downtime**: You can update applications without affecting your availability. Some Pods are updated, while others are running, so the service is not interrupted.
2. **Minimal Risk**: Instead of having to take the site down completely and install it from scratch, it is possible to update Pods one at a time or in small batches, which enables you to verify the new version by keeping the old version still serving traffic. If something doesn't happen as it should, Kubernetes has the capability of automatically doing a reverse operation.
3. **Automatic Scaling**: In the course of the rolling update, Kubernetes guarantees that the actual number of the running Pods matches the right one thus, your application can expand or shrink as per requirement.

### **What is a Rolling Update in Kubernetes?**

A **Rolling Update** is a Kubernetes Deployment strategy that lets updated Pods be incrementally added. Kubernetes regulates the implementation of the new version providing that there are enough pods to go through the update process.

The rolling update process works as follows:
1. **Old Pods are terminated**: Kubernetes removes the old Pods gradually and replaces them with the new ones.
2. **New Pods are created**: Kubernetes generates new Pods that contain the updated container image (or new version of the application).
3. **Progressive replacement**: Just a few Pods at a time can be updated to avoid service disruptions. This is determined by the **maxSurge** and **maxUnavailable** values.


![Rolling update](https://www.bluematador.com/hs-fs/hubfs/blog/new/Kubernetes%20Deployments%20-%20Rolling%20Update%20Configuration/Kubernetes-Deployments-Rolling-Update-Configuration.gif?width=1600&name=Kubernetes-Deployments-Rolling-Update-Configuration.gif)
Source: https://www.bluematador.com/hs-fs/hubfs/blog/new/Kubernetes%20Deployments%20-%20Rolling%20Update%20Configuration/Kubernetes-Deployments-Rolling-Update-Configuration.gif?width=1600&name=Kubernetes-Deployments-Rolling-Update-Configuration.gif 

### **Update Strategies in Kubernetes**

Kubernetes provides several strategies for managing updates, each with its own use cases and advantages.

#### **1. Rolling Update (Default Strategy)**

This is the default update strategy for Deployments in Kubernetes. It works by gradually replacing old Pods with new ones, maintaining the desired number of Pods running at all times.

- **How it works**: Kubernetes updates the specified number of Pods while delivering the application availability during the update process.
- **Configuration**: The pacing of the update can be altered by changes in the `maxSurge` and `maxUnavailable` fields in the Deployment spec.

##### Example:
```yaml
spec:
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
```
- **maxSurge**: The maximum number of Pods you want to create in addition to the desired number of Pods during an update.
- **maxUnavailable**: The maximum number of Pods you can be unavailable due to the update.

#### **2. Recreate Strategy**

Use the **Recreate Strategy**, when desired. In this case, all of the pods are terminated and then replaced one by one. This way, you can run only one version of your application that isn´t compatible if you can't put it on at the same time as another, but of course, there is a time that it doesn´t work while you update it.

- **How it works**: The first stage is that Kubernetes removes all the old pods and then creates the ones that have the new version. As the result, some period will exist when no pods can be created.

##### Example:
```yaml
spec:
  strategy:
    type: Recreate
```

#### **3. Blue-Green Deployment**

While Kubernetes doesn’t naturally support the **Blue-Green Deployments**, you can undertake additional tasks to have it working. By using this method, two development spaces colored blue and green are created on the server. The previous version has a home in one space, and the new one is brought into the other case. The process finally the new version is switched from blue to green traffic. This process requires manual interaction, without any automation. This automation includes manual error correction that enables no system failure during this process.

- **How it works**: Two separate sets of pods are in operation (old and new version). They are both running at the same time. Pod is required by the Service to modify the indication to a new set of the pods.
- **Advantages**: Deploying both the latest and the previous versions means then running two environments in parallel, so that the customers can have the current version and the green new one at the same moment. Normally, if the rollbacks are needed this is a simple step as the old environment is still available.

##### Blue-Green Deployment Process:
1. Deploy the new version to the green environment.
2. Run tests and ensure the green environment works properly.
3. Switch the traffic to the green environment.
4. Optionally, scale down the blue environment.

![blue-green deployment](https://miro.medium.com/v2/resize:fit:1400/1*QJkMQzAVx8YgQRPBIaUifg.gif)
source: https://miro.medium.com/v2/resize:fit:1400/1*QJkMQzAVx8YgQRPBIaUifg.gif 
#### **4. Canary Deployment**

**Canary Deployments** are the gradual rolling out of a new version to a small subset of users (canaries) before a full-scale release. This helps you to test the new version in production with a limited number of users and reduce the risk of a failed deployment affecting the whole application.

- **How it works**: You create a small subset of Pods that are running the new version, while the majority of Pods are still running the old version. If everything goes well, you can then gradually increase the number of Pods that run the new version.

![canary deployment](https://i.sstatic.net/zcXYE.gif)
source: https://i.sstatic.net/zcXYE.gif 

##### Example:
You could scale up the Deployment gradually:
```bash
kubectl scale deployment my-app --replicas=10
kubectl set image deployment/my-app my-app-container=my-app:v2
```

The new version would be rolled out incrementally by scaling up Pods in steps.

### **Managing Rolling Updates**

To manage Rolling Updates, you can use several kubectl commands to monitor and control the update process.

1. **Monitor Rollout Status**
   Use the following command to check the status of a rollout:
   ```bash
   kubectl rollout status deployment/my-app
   ```
   This will show you whether the deployment is complete, still in progress, or if there are issues.

2. **Pause and Resume Rollout**
   If you need to stop the update for any reason, you can pause the rollout:
   ```bash
   kubectl rollout pause deployment/my-app
   ```
   To resume the rollout:
   ```bash
   kubectl rollout resume deployment/my-app
   ```

3. **Rollback to a Previous Version**
   If something goes wrong during the update, you can easily roll back to the previous version:
   ```bash
   kubectl rollout undo deployment/my-app
   ```


### **Key Takeaways**
- **Rolling Updates** allow you to update your application with zero downtime by updating Pods incrementally.
- Kubernetes supports different update strategies: Rolling Update (default), Recreate, Blue-Green, and Canary deployments, each with its own use case.
- You can control the update process through `maxSurge`, `maxUnavailable`, and other settings.
- Rollout management tools like `kubectl rollout status`, `kubectl rollout pause`, and `kubectl rollout undo` are essential for controlling updates and ensuring smooth application deployment.

## **Suggested Reading**

1. [Kubernetes Rolling Update Documentation](https://kubernetes.io/docs/tutorials/kubernetes-basics/update-update/)
2. [Kubernetes Deployment Strategies](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#deployment-strategies)
3. [Blue-Green Deployment](https://martinfowler.com/bliki/BlueGreenDeployment.html)

