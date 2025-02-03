## Deploy Voting App on Kubernetes

Deploy Voting App on k8s with desired services.

## Prerequisite

- Make sure the Kubernetes cluster is up and running
- The code for this application can be accessed [here](https://github.com/saurabh-coding-dojo/voting-app-k8s)

Steps to follow
- Create five manifest files to deploy all five microservices as Kubernetes pods.
- Deploy 1 replica of each pod.
- Enable connectivity as required. Look at the diagram below.
- Create a NodePort Service to expose the “voting application”
- Create a NodePort Service to expose the “result application”
- Create a ClusterIP Service to connect redis database to the voting and worker app. Name the service as redis
- Create a ClusterIP Service to connect PostgreSQL database to the worker and voting app. Name the service as db
- Create a load balancer to expose the voting and result application.)

Architecture Diagram –

![architecture](https://uptut.gitbook.io/~gitbook/image?url=https%3A%2F%2Flh7-us.googleusercontent.com%2FV1_r2v2fgueP4NRvE6-x6PUVP_rNFB503ria_KIXq7pXUYteY7ntAoACvlRALcLopx0g_dnnqoVLH9ssdib1sRX1-l98hczWEb47EfFuoiyXNCtqggwwgkuxq8s94NwOCnpqWFScFKTau6k8qGlkWQ&width=300&dpr=4&quality=100&sign=e5197310&sv=2)

The solution to this task can be accessed [here](https://github.com/saurabhd2106/votinga-app-solution-4sep/tree/main/v1)
