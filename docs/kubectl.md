# Kubectl

The following are cases for using Kubectl

## Creating a Simple Application

In this scenario, we are creating an app based on an image named `k8s.gcr.io/echoserver:1.4`. The steps involved are:

1. Create deployment call **hello-node** based on image k8s.gcr.io/echoserver:1.4. `kubectl create deployment hello-node --image=k8s.gcr.io/echoserver:1.4`
1. Create a service Expose deployment named **hello-node**, exposing port 8080 to the outside world. `kubectl expose deployment hello-node --type=LoadBalancer --port=8080`
1. Provide access to an applications. `kubectl port-forward service/hello-node 7080:8080`

## Inspecting and Managing Applications

Deployment related
1. View deployment. `kubectl get deployments`
1. View pod. `kubectl get pods`
1. Delete deployment. `kubectl delete deployment hello-node`

Service related
1. Delete services. `kubectl delete service hello-node`
1. View service. `kubectl get services`