## Project - Deploy a 3-tier application on Kubernetes
In this lab session, deploy a 3 tier application on Kubernetes

The sample application has a backend application built-in “.Net core”. A frontend application was built with HTML, CSS, and JavaScript, and the database used Postgres.

Application link -[ 3 Tier Web Application]([url](https://github.com/saurabhd2106/3-tier-application))

- The backend application code can be accessed under Basic3Tier.API repo.
- The frontend application code can be accessed under Basic3Tier.UI repo.
- The database is a "PostgreSQL" database.

## TASK 1 - Containers all microservices
- Create the containers of the frontend, backend and database.
- Make sure the application is running with docker deployment and all the communication is also working.

## TASK 2 - Deploy the application on Kubernetes
- Create three deployment manifest files, one each for frontend, backend, and database.
- Deploy one pod of frontend, three pods of backend and one pod of the database.
- Create a NodePort Service to expose “frontend application”
- Create a NodePort Service to expose “backend application”
- Create a ClusterIP Service to connect frontend and backend applications
- Create a ClusterIP Service to connect the backend with the database.
- Create a load balancer to expose the frontend application.
- Use Persistent Volume to store the Postgres data.
