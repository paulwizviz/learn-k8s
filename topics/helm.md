# Helm

Think of Helm like "apt" or "yum" for Linux, but for Kubernetes. It allows you to easily install, update, and manage applications on your Kubernetes cluster.

Essentially, Helm helps to:

* Automate the deployment of applications.
* Reduce the complexity of managing Kubernetes manifests.
* Provide a way to share and reuse Kubernetes applications.

## Helm Charts

A Helm chart is essentially a collection of files organized in a specific way that describes a set of Kubernetes resources. 

A Helm chart resides in a directory, and that directory's name is the chart's name. Inside that directory, you'll generally find these core files and directories:

* `Chart.yaml`:
    * This is a required file that contains metadata about the chart, such as its name, version, and description.   
    * It provides essential information for Helm to manage the chart.
    * This file defines essential chart metadata.   
    * Key fields include:
        * `apiVersion`: The Helm API version.
        * `name`: The chart's name.
        * `version`: The chart's version.
        * `description`: A brief description of the chart.
        * `dependencies`: A list of dependent charts. 
* `values.yaml`:
    * This file holds the default configuration values for the chart.   
    * Users can override these values during installation or upgrade to customize the deployment.
```YAML
    replicaCount: 3
    image:
      repository: nginx
      tag: stable
      pullPolicy: IfNotPresent
    service:
      type: ClusterIP
      port: 80 
```
* `templates/` directory:
    * This directory contains the Kubernetes manifest files (YAML files) that define the resources to be deployed.   
    * These files often use Go templating to allow for dynamic configuration based on the values provided in values.yaml.
    * Inside the templates directory you will often find files such as:
        * `deployment.yaml`
        * `service.yaml`
        * `ingress.yaml`
        * `configmap.yaml`
        * `secret.yaml`
        * `_helpers.tpl`: This file contains template helpers that can be reused throughout the templates.
        * `NOTES.txt`: This file contains notes that are displayed to the user after the chart is installed.
    * Kubernetes manifest files are written here, and Helm's templating engine processes them -- [The Chart Template Developer's Guide](https://helm.sh/docs/chart_template_guide/).   
    * Go templating allows you to:
        * Inject values from values.yaml.
        * Use conditional logic.
        * Iterate over lists.
    * For example in a deployment.yaml file you might see.
    * `replicas: {{ .Values.replicaCount }}`
    * This will inject the replica count from the values.yaml file.
* `charts/` directory (optional):
    * This directory is used to store dependent charts (subcharts).   
    * If your chart relies on other charts, you can include them here.

## Releases

A release is an instance of a chart running in a Kubernetes cluster. Every time you install a chart, you create a release. This allows you to have multiple instances of the same application running with different configurations.

## Repositories

Helm charts are stored in repositories, which are like online libraries. You can find and download pre-built charts from public repositories or create your own private ones.

## References

* [Helm](https://www.redhat.com/en/topics/devops/what-is-helm)
* [Secure Helm: Kubernetes Deployment Best Practices](https://www.plural.sh/blog/helm-chart)
