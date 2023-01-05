---
---

# Kubernetes

## Plan 🕙
- [ ]  Prerequisites
    - [x]  What is container
    - [ ]  Service Discovery
    - [x]  Networking Basics
- [x]  What is Kubernetes
- [ ]  K8s components
    - [ ]  pods, nodes, services
    - [ ]  Kubeconfig
    - [ ]  Objects, Resources
- [ ]  Local Setup
    - [ ]  Ways of setup
    - [x]  Minikube
    - [ ]  Cluster
- [ ]  K8s Architecture 👎
- [ ]  Kubernetes API
    - [ ]  kubectl
- [ ]  Advance Topics
    - [ ]  Networking
    - [ ]  Storage
    - [ ]  Monitoring
    - [ ]  Workflows

## Index
- [What is Kubernetes](what-is-kubernetes)
- [K8s components](k8s-components)
- [Local Setup](local-setup)

## What is Kubernetes

- A containers (can be any like Docker managed) archestration tool.
- With rise of microservices & distributed systems, managing all containers has become difficult & K8s helps there.

### How K8s Helps
- Manage scalability in distributed systems
- Manage availability
- Manage disaster recovery etc.

## K8s components
**K8s Cluster**: Group of servers where all of the application instances / microservices are hosted.

**Node**: One of the server part of k8s cluster.

**pod**:
- Smallest part of components
- Kind of wrapper over container
- Generally contains single app image. But can also host multiple apps.
    - e.g. in-memory cache sitting near services instance.
- pod is introduced to abstract out concept of containers. This removes tight coupling with any of the container provider like docker.
- Single node may contain multiple pods, say **MyApp** pod & **DB** pod.
- pod is ephemeral in nature, means it dies anytime without recording state / storage etc.

**IP**:
- Each pod has its own IP address local to node.

**Service**:
- When a pod dies, new pod will have new IP address.
- In such cases other pods communicating to this with its IP needs to change thier IP URL. This isnt feasible.
- Service component help avoid this issue. Service is loosely coupled with pod & knows new IP assosiated with its pod and keeps a constant IP address for other pods to connect.

**Ingress**
- pods can communicate with each other with their internal services.
- when pods need to be exposed externally ingress is used.

**Volume**
- Since pods are ephemeral in nature, data or state is lost when it dies.
- imagine a DB loosing its data wheb DB pod dies.
- In such cases k8s needs permanent storage and volume component helps with that.
- Which can be either local or external storage

**ConfigMap**
- Imagine DB URL of DB is changed. Now app pod needs to be changed to accept this change.
- This needs entire SDLC to get changes reflected.
- ConfigMap is component which sits inside node where such config information can be stored and shared with all the pods within node.

**Secrets**
- Secrets component is similar to configMap which is only used to store secrets and follows encryption way of storing properties

## Local Setup

### Minikube
Make sure docker daemon is running.
- Download linux minikube version
```console
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```

- Install minikube
```console
# Path can be any executable standard path.
# For Sudo access
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# For Local User access
KUBECONFIG=$HOME/.kube/my_minikube_config
minikube start --memory 8192 --cpus 4
```

#To access the Kubernetes Dashboard, run . to get your dashboard up in background
```console
minikube dashboard &

minikube docker-env
```


👷 WORK IN PROGRESS
