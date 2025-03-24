# DevOps

The core steps in DevOps are:

1. Create a Deployment: You define the desired state of your application (e.g., how many replicas of your pod should run, what container image to use).
2. Kubernetes Schedules Pods: Kubernetes places the pods onto the nodes based on resource availability and other factors.
3. Access the Application: You create a Service to expose your application.
Kubernetes Manages the Application: Kubernetes continuously monitors the state of your application and makes adjustments as needed (e.g., restarting failed pods, scaling up or down).

## Minimum Deployment

Here are example scripts of a minimum deployment:

* A [deployment](../deployment/basic/deployment.yaml) script
* A [service](../deployment/basic/service.yaml) script

## References

* [Kubernetes YAML](https://www.youtube.com/watch?v=qmDzcu5uY1I)
* [Full Application deployment example](https://www.youtube.com/watch?v=EQNO_kM96Mo)