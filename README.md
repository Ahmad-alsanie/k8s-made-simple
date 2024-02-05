## Kubernetes Made Simple
Is a straight forward tutorials on what you need to know as a software engineer to use Kubernetes

### Book Definition
Kubernetes is an open-source container orchestration system for automating software deployment, scaling, and management.

### How to navigate this repository
A side from impracticable knowledge included this read me, I have added practical real-world examples of k8s main features.
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