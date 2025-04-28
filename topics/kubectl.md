# Kubectl

The following summarises `kubectl` operations.

## Topics

* [`kubectl` Configuration (kubeconfig)](#kubectl-configuration-kubeconfig)
* [Creating a Simple Application](#creating-a-simple-application)
* [Inspecting and Managing Applications](#inspecting-and-managing-applications)
* [Kubectl Context](#kubectl-context)

## `kubectl` Configuration (kubeconfig)

`kubectl` uses a configuration file (usually ~/.kube/config) to store connection details for one or more Kubernetes clusters.  This file is called a kubeconfig file.  It contains information like:

* **Clusters**: The API server addresses and certificates for your Kubernetes clusters.
* **Users**: Authentication credentials for accessing the clusters.
* **Contexts**: A combination of a cluster and a user. You use contexts to switch between different clusters.

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

## Kubectl Context

* [Context Settings](#kubectl-context-settings)
* [Context operations](#kubectl-context-operations)

### Kubectl context settings

#### Minikube

* **STEP 1:** Run the command `minikube config use-context minikube`. This command configures `kubectl` to interact with your Minikube cluster.
* **STEP 2:** Run the command `kubectl config current-context`, which should now show 'minikube'.

### Kubectl context operations

You use the `kubectl config use-context` command followed by the name of the context you want to switch to.

Here's the basic syntax:

```sh
kubectl config use-context <context-name>
```

**Example:**

Let's say you have two contexts configured in your ~/.kube/config file: minikube and production. To switch to your Minikube cluster, you would run:

```sh
kubectl config use-context minikube
```

To switch back to your production cluster, you would run:

```sh
kubectl config use-context production
```

You can list all the configured contexts using the following command:

```sh
kubectl config get-contexts
```

This will output a table showing the available contexts, with an asterisk (*) marking the currently active context.

In summary, to switch contexts with `kubectl`:

1. Know the name of the context you want to switch to (you can find this using `kubectl config get-contexts`).
1. Use the `kubectl config use-context` command followed by the context name.

After running the `use-context` command, all subsequent `kubectl` commands will be directed to the cluster associated with that context.
