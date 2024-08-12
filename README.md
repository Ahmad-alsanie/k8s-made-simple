## Kubernetes Made Simple
Is a straight forward tutorials on what you need to know as a software engineer to use Kubernetes

### Book Definition
Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.

### How to navigate this repository
A side from impracticable text book definitions included in this read me, I have added practical real-world examples of k8s main features.
Each package contains a real world configurations that will help you to get going with k8s.

### Before you start
Before diving into Kubernetes, ensure you have a solid understanding of container technology, primarily Docker. 
Containers package software so it can run anywhere, solving the "it works on my machine" headache.

Learn Docker: Understand how to create, run, and manage containers. Familiarize yourself with Dockerfiles, images, and containers.
Practice: Build a simple application (e.g., a Java Spring Boot or Kotlin application) and containerize it using Docker.

### Table of Content
- [Pods](#Pods)
- [Services](#Services)
- [Deployments](#Deployments)
- [ConfigMaps and Secrets](#ConfigMaps-and-Secrets)
- [Ingress](#Ingress)
- [Persistent Volumes](#Persistent-Volumes)
- [StatefulSet](#StatefulSet)
- [Deploy your app](#Deploy-your-application)
- [Commands - what you need to  manage resources and troubleshoot issues](#Commands)


### Pods
A Pod is the smallest deployable unit in Kubernetes, which can run one or more closely related containers. 
Pods encapsulate containers, storage resources, a unique network IP, and options that govern how the container(s) should run.

See: [pod.yaml](./src/main/java/com/sanie/pods)

### Services
A Service in Kubernetes is an abstract way to expose an application running on a set of Pods as a network service. 
With Kubernetes, you don't need to modify your application to use an unfamiliar service discovery mechanism. 
Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods and can load-balance across them.

See: [services.yaml](./src/main/java/com/sanie/services)

### Deployments
A Deployment provides declarative updates for Pods and ReplicaSets. 
You describe a desired state in a Deployment, and the Deployment Controller changes the actual state to the desired state at a controlled rate. 
You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

See: [deployments.yaml](./src/main/java/com/sanie/deployments)

### ConfigMaps and Secrets
ConfigMaps allow you to decouple configuration artifacts from image content to keep containerized applications portable. 
Secrets are similar but are used to store and manage sensitive information, such as passwords, OAuth tokens, and ssh keys.

see: [config-maps.yaml](./src/main/java/com/sanie/configmaps)

### Ingress
Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster. 
Traffic routing is controlled by rules defined on the Ingress resource.

see: [ingress.yaml](./src/main/java/com/sanie/ingress)

### Persistent Volumes
PVs and PVCs provide a method for users and administrators to abstract details of how storage is provided from how it is consumed. 
A PV is a piece of storage in the cluster, while a PVC is a request for storage by a user.

see: [pv.yaml](./src/main/java/com/sanie/pv)

### StatefulSet
StatefulSets are the workload API object used to manage stateful applications. 
They provide unique, persistent identifiers and stable hostnames for each Pod, making them suitable for applications that require stable, persistent storage.

see: [stateful-set.yaml](./src/main/java/com/sanie/stateful)

### Deploy your application
This yaml describes the desired state of your application deployment, including the Docker image to use, the number of replicas, and more.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: myapp:latest
        ports:
        - containerPort: 80
```

Apply the Deployment: Use ```kubectl apply -f deployment.yaml``` to create the deployment in your cluster.

Expose the Deployment as a Service to make your application accessible, expose it through a Service:

```shell
kubectl expose deployment myapp-deployment --type=LoadBalancer --name=myapp-service
```

Access Your Application: If using Minikube, use ```minikube service myapp-service``` to open the application in a browser.

### Commands

1- Cluster Management

```kubectl cluster-info``` Display cluster info.

```kubectl get nodes``` List all nodes in the cluster.

```kubectl config view``` Show current context.

```kubectl config use-context <context-name>``` Switch between contexts (clusters).

2- Working with Applications & Managing Deployments

```kubectl create -f <deployment.yaml>``` Create a deployment using a YAML file.

```kubectl get deployments``` List all deployments.

```kubectl rollout status deployment/<deployment-name>``` Get the rollout status of a deployment.

```kubectl set image deployment/<deployment-name> <container-name>=<new-image>``` Update the deployment with a new image.

```kubectl rollout undo deployment/<deployment-name>``` Roll back to the previous deployment.

3- Working with Pods

```kubectl get pods``` List all pods.

```kubectl describe pod <pod-name>``` Get detailed information about a pod.

```kubectl logs <pod-name>``` View logs for a specific pod.

```kubectl exec -it <pod-name> -- /bin/bash``` Execute an interactive bash shell in the specified pod.

4- Managing Services

```kubectl get services``` List all services in the namespace.

```kubectl expose deployment <deployment-name> --type=LoadBalancer --name=<service-name>``` Expose your deployment as a service.

```kubectl delete service <service-name>``` Delete a service.

5- Configurations & Secrets

```kubectl create configmap <configmap-name> --from-file=<path-to-file>``` Create a ConfigMap from a file.

```kubectl create secret generic <secret-name> --from-literal=key=value``` Create a secret from a literal value.

6- PV

```kubectl get pv``` List all Persistent Volumes.

```kubectl get pvc``` List all Persistent Volume Claims.

7-Debugging

```kubectl describe pods <pod-name>``` Show detailed information about a pod, useful for debugging.

```kubectl get pods --all-namespaces``` List all pods in all namespaces, useful for getting an overview of what’s running.

```kubectl logs <pod-name>``` Fetch logs of a pod.

```kubectl exec -it <pod-name> -- <command>``` Execute a command in a container.

8- Advanced Ops -Scaling, labeling, namespaces-

```kubectl get namespaces``` List all Kubernetes namespaces.

```kubectl create namespace <namespace-name>``` Create a new namespace.

```kubectl label pods <pod-name> <label-key>=<label-value>``` Add a new label to a pod.

```kubectl annotate pods <pod-name> <annotation-key>=<annotation-value>``` Add a new annotation to a pod.

```kubectl scale deployment <deployment-name> --replicas=<num-replicas>``` Scale a deployment to the specified number of replicas.

```kubectl autoscale deployment <deployment-name> --min=<min-pods> --max=<max-pods> --cpu-percent=<target-CPU-utilization>``` Automatically scale the number of pods in a deployment.

9- Resource Management

```kubectl apply -f <file.yaml>``` Apply a configuration to a resource from a file.

```kubectl delete -f <file.yaml>``` Delete resources defined in a YAML file.

```kubectl describe quota``` Show detailed information about applied quotas.

```kubectl describe limitrange``` Show detailed information about applied limit ranges.

## Contributing

Contributions are welcome! If you have improvements or additions, please submit a pull request or open an issue.

-------------------------------------------------------------
Happy coding! 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
