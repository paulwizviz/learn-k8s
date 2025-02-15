# Using minikube and kubectl

This is an implementation using minikube based on this example [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)

## Minikube operations

1. Start minikube.
   * With default vm `minikube start`
   * With virtual box `minikube start --driver=virtualbox`
1. Opening dashboard. `minikube dashboard`
1. Addons. 
   * List addons. `minikube addons list`
   * Enabling addons. `minikube addons enable <addons name>`
   * Disabline addons. `minikube addons disable <addons name>`
1. VM operations.
   * Stop vm. `minikube stop`
   * Delete vm. `minikube delete`

## Managing Docker Images

The following are options for managing Docker Images:

1. `minikube image load` (Recommended for Minikube): This is the easiest and most efficient way for Minikube.  It loads the image directly into Minikube's Docker daemon.

```bash
minikube image load my-web-app:v1
```
> **NOTE**: my-web-app:v1 is an example image prebuilt and store in Docker deamons.

After running this command, Minikube will have the image available, and your Kubernetes deployments can reference it.  This is the recommended approach for local development with Minikube.

2. Building the image inside Minikube: You can use the docker CLI within the Minikube VM to build the image.  This requires some setup but can be useful.

* First, you need to configure your local Docker client to talk to the Docker daemon inside Minikube:
```bash
eval $(minikube docker-env)
```
This command sets the necessary environment variables.  Make sure to run this command in any terminal where you want to use the Docker CLI to interact with Minikube's Docker.

* Then, you can build your image as usual:

```bash
docker build -t my-web-app:v1 .
```
Now, the image is built inside Minikube's Docker, and your Kubernetes deployments can reference it.

3. Using a local registry (More complex, less common for Minikube): You can set up a local Docker registry (e.g., using docker-compose or a simple Docker container) and push your images there.  Minikube can then pull from this local registry.  This is more complex than the other options and is generally not recommended for simple Minikube setups.  It's more relevant for multi-node clusters or CI/CD pipelines.

Which method should you use?

For Minikube development, minikube image load is the strongly recommended approach. It's the simplest, fastest, and most efficient.  It avoids the complexities of setting up a local registry or building inside the VM.
