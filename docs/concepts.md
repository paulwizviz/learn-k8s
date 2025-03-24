# Concepts

Kubernetes (often abbreviated as K8s) is an open-source system for automating deployment, scaling, and management of containerized applications.  Think of it as an orchestrator for containers.  It takes care of things like:   

* **Scheduling:** Deciding where your containers run.
* **Scaling:** Increasing or decreasing the number of running containers.
* **Service Discovery:** How your applications find each other.
* **Load Balancing:** Distributing traffic across your containers.
* **Rolling Updates:** Updating your application with minimal downtime.
* **Self-Healing:** Restarting failed containers.

## Core Steps in Deployment

1. Create a Deployment: You define the desired state of your application (e.g., how many replicas of your pod should run, what container image to use).
2. Kubernetes Schedules Pods: Kubernetes places the pods onto the nodes based on resource availability and other factors.
3. Access the Application: You create a Service to expose your application.
Kubernetes Manages the Application: Kubernetes continuously monitors the state of your application and makes adjustments as needed (e.g., restarting failed pods, scaling up or down).

## Example: Deploying a Simple Web Application

Let's imagine you have a simple web application packaged in a Docker container called my-web-app:v1.

**STEP 1:** Deployment YAML: You would create a YAML file (e.g., deployment.yaml) that defines the deployment:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-web-app
spec:
  replicas: 3 # Run 3 replicas of the pod
  selector:
    matchLabels:
      app: my-web-app
  template:
    metadata:
      labels:
        app: my-web-app
    spec:
      containers:
      - name: my-web-app
        image: my-web-app:v1
        ports:
        - containerPort: 8080 # The port your application listens on
```

**STEP 2:** Apply the Deployment: You would use the kubectl apply -f deployment.yaml command to create the deployment in your Kubernetes cluster.

**STEP 3:** Service YAML:  You'd create a service to expose the application (e.g., service.yaml):

```YAML
apiVersion: v1
kind: Service
metadata:
  name: my-web-app-service
spec:
  selector:
    app: my-web-app
  ports:
  - protocol: TCP
    port: 80 # The port you access the service on
    targetPort: 8080 # The port the container listens on
  type: LoadBalancer # Expose the service externally (if supported by your cluster)
```

**STEP 4:** Apply the Service: kubectl apply -f service.yaml

## Minimum Deployment

Here are example scripts of a minimum deployment:

* A [deployment](../deployment/basic/deployment.yaml) script
* A [service](../deployment/basic/service.yaml) script

## References

* [Kubernetes YAML](https://www.youtube.com/watch?v=qmDzcu5uY1I)
* [Full Application deployment example](https://www.youtube.com/watch?v=EQNO_kM96Mo)