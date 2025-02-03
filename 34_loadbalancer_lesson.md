# LoadBalancer Service in Kubernetes

## Overview  
Services are the building blocks of communication in Kubernetes which enables communication within the cluster as well as outside access. **NodePort** is a type of service that enables you to expose the service via a static port on every node while LoadBalancer is a type of service that goes further by integrating with external load balancing solutions. In the modern world, businesses are in competition with one another; for this reason, services like LoadBalancer that expose applications to the internet traffic with more efficiency, higher availability, and better scalability are particularly useful. In this lesson, we will take a closer look at the LoadBalancer service type in Kubernetes, its use cases, and the working of the same.

## Lesson Outcomes  
By the end of this lesson, you will:  
- Understand the purpose and use cases of the **LoadBalancer** service type.
- Learn how **LoadBalancer** integrates with cloud providers and external load balancers.
- Know how to configure and use a **LoadBalancer** service in Kubernetes.

## Explanation

### Why LoadBalancer is Needed  
NodePort in Kubernetes is an option to expose services externally on a specific port of all nodes, but it does not have an in-built way for traffic distribution or more complex load balancing. For numerous, or even most, applications that are ready for production, you now require a more perfect approach of sending load across the new instances and they will be always up and running.

Certainly, you can either spin up external load balancers or employ solutions like Ingress, but LoadBalancer  is the simplest way to interface with external load-balancing services in the cloud. It provides the possibility that you can get an external IP that routes traffic to your service automatically, and besides, the cloud provider is the one who handles the load balancing.

#### Key Benefits of LoadBalancer Over NodePort:
- **Automatic Load Balancing**: It manages the traffic distribution across the service using the external load balancer it created.
- **High Availability**: The cloud provider takes care of the availability of the load balancer, thus, enabling the high availability and fault tolerance of the service.
- **Ease of Use**: Since Kubernetes connects to the load balancing solution of your cloud provider directly, you need not do so. Thus, you will not have to deal with external load balancers manually.

### How Does LoadBalancer Work?  
When you create a **LoadBalancer** service in Kubernetes, the platform calls an API (Amazon Web Services, Google Cloud Platform, or Microsoft Azure) of the selected cloud provider and asks for a new external load balancer to turn on the newly created application. There will be an external IP address that the clients can use coming from this load balancer which means external clients would get to running services through that route. Subsequently, the cloud provider's load balancer handles client requests on the grassroots by ensuring that the requests are equally distributed to the appropriate Pods behind the service as per the set-up (Round-robin, least connections, etc.)

Here’s how it works step-by-step:
1. **Service Creation**: You set a **LoadBalancer** service by writing its definition just like that of the ClusterIP or NodePort with the type set to LoadBalancer.
2. **Cloud Integration**: Once you create the configuration, Kubernetes talks to your cloud provider’s API and tells it to start a new load balancer.
3. **External IP Allocation**: The cloud service provider assigns a public IP address to the load balancer.
4. **Traffic Routing**: Traffic from external clients is sent to the load balancer, which then forwards it to one or more Pods in the Kubernetes cluster.


#### Example:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-web-app-service
spec:
  selector:
    app: my-web-app
  ports:
    - port: 80
      targetPort: 8080
  type: LoadBalancer
```
In this example:
- The service exposes the application on port **80**.
- The cloud provider automatically provisions a load balancer and assigns it an external IP.
- Traffic to that external IP is forwarded to the Pods that match the selector `app=my-web-app` on port **8080**.

### When to Use LoadBalancer?  
A **LoadBalancer** service is most suitable for doing the following:
1. **High Availability**: To guarantee that your service is still available and can scale in case of failure, you should horizontally partition the traffic among various Pods or nodes while making necessary adjustments to the deployed replicas.
2. **External Access**: If your service is expected to become externally available without any action of manually creating, assigning and updating IP address, creating instances, or performing physical system maintenance or reconfiguration of the firewall, then you are looking for the cloud computing model of Xaas that may be the right one.
3. **Cloud-Native Applications**: One of the benefits of using **LoadBalancer** services for traffic distribution in the cloud is that it is Amazon AWS, Google Cloud Platform (GCP), or Microsoft Azure among others that provide the capacity to use their cloud infrastructure for load balancing.
4. **Simplified Management**: You need a seamless and efficient solution where Kubernetes and your cloud provider automatically manage the traffic and load distribution.

#### Example Use Cases:
- **Web Applications**: Running the cluster of multiple pods as well as regulating the traffic of incoming requests to each pod automatically allows you to host a web application that will be run by the webserver based on your necessity.
- **APIs**: When adjusting the creation of a new API via the web, you should have the option of allowing single or multiple server applications and then setting the necessary load balancing software so that the server processes resources to existing servers according to their workloads.
- **Microservices**: In a microservices setup that consists of a collection of small services that communicate and are independently deployable, the **LoadBalancer** service is something that helps with the arrangement of the communication between each service and the relaying of the traffic to each service.

### How to Configure LoadBalancer  
In order to have a **LoadBalancer** service, you have to declare the service as a type **LoadBalancer** in a service file. After setting this option, Kubernetes automatically creates the required external load balancer, and the cloud provider will handle its operation.

Here's a simple YAML example for creating a LoadBalancer service:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-api-service
spec:
  selector:
    app: my-api
  ports:
    - port: 80
      targetPort: 8080
  type: LoadBalancer
```

- **Selector**: The service will target Pods with the `app: my-api` label.
- **Ports**: Exposes the service on port **80** within the cluster and forwards traffic to port **8080** on the Pods.
- **LoadBalancer**: This type ensures an external load balancer is provisioned by the cloud provider.

Once the service is created, you can retrieve the external IP address assigned to the load balancer:
```bash
kubectl get svc my-api-service
```
You will see an output similar to:
```
NAME              TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)        AGE
my-api-service    LoadBalancer   10.0.0.100    34.67.23.45     80:30792/TCP   10m
```
In this case, `34.67.23.45` is the external IP address where your service is accessible.

### Benefits of LoadBalancer  
1. **Automatic Traffic Distribution**: Traffic coming from the internet is automatically distributed to a different set of your pods connected together in a service for load balancing.
2. **High Availability**: Remarkable high Availability is the feature of which load balancer is most proud of. Thus, the cloud provider's load balancer can then virtually "never fail" and scales out automatically.
3. **No Need for Manual Setup**: Setup of load balancing does not require user intervention anymore, it is handled by Kubernetes and the cloud provider, and thus is easier to work with in the external world.
4. **Scalability**: Traffic towards a minimum request, in other words traffic to right pods, splitting traffic evenly so the services can be scaled are some of the purposes of load balancing.

### Limitations of LoadBalancer  
1. **Cloud Provider Dependency**: The **LoadBalancer** service type depends on your cloud provider’s infrastructure. If you’re running Kubernetes on-premise or on unsupported cloud providers, this feature might not be available.
2. **Cost**: Cloud providers often charge for external load balancers, so this option can increase costs compared to other types of services like **NodePort** or **ClusterIP**.
3. **Limited Configuration**: The configuration options for load balancers are relatively limited compared to using a dedicated load balancing solution or Ingress controllers.

### Suggested Reading  
1. [Kubernetes Documentation on Services](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)  
2. [How Kubernetes Integrates with Cloud Load Balancers](https://cloud.google.com/kubernetes-engine/docs/concepts/service#loadbalancer)  
3. [Kubernetes Networking Guide](https://www.oreilly.com/library/view/kubernetes-up-and/9781098110205/ch04.html)  
