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
    - [x]  pods, nodes, services
    - [ ]  Kubeconfig
    - [ ]  Objects, Resources
- [x]  Local Setup
    - [x]  Ways of setup
    - [x]  Minikube
    - [ ]  Cluster 👎
- [x]  K8s Architecture
- [x]  Kubernetes API
    - [x]  kubectl
    - [ ]  K8s UI 👎
- [ ]  Advance Topics
    - [ ]  Networking
    - [ ]  Storage
    - [ ]  Monitoring
    - [ ]  Workflows

## Index
- [What is Kubernetes](what-is-kubernetes)
- [K8s components](k8s-components)
- [K8s Architecture](k8s-architecture)
- [Local Setup](local-setup)

## What is Kubernetes
- A containers (can be any like Docker managed) archestration tool.
- With rise of microservices & distributed systems, managing all containers has become difficult & K8s helps there.

### How K8s Helps
- Manage scalability in distributed systems
- Manage availability
- Provides vertual network for distributed application for easy management.
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
- Each pod has its own IP address internal to K8s cluster.

**Service**:
- When a pod dies, new pod will have new IP address.
- In such cases other pods communicating to this with its IP needs to change thier IP URL. This isnt feasible.
- Service component help avoid this issue. Service is loosely coupled with pod & knows new IP assosiated with its pod and exposes static IP address for other pods to connect.
- Service component also acts as load balancer, imagine we have replica of our pod which also connects to same service component. Now Service component receives requests and routes to less busy pod instance.

**Ingress**
- pods can communicate with each other with their internal services / pods.
- when pods need to be exposed externally ingress is used.

**Volume**
- Since pods are ephemeral in nature, data or state is lost when it dies.
- imagine a DB loosing its data wheb DB pod dies.
- In such cases k8s needs permanent storage and volume component helps with that.
- Which can be either local or remote storage which is connected to K8s cluster

**ConfigMap**
- Imagine DB URL of DB is changed. Now app pod needs to be changed to accept this change.
- This needs entire SDLC to get changes reflected.
- ConfigMap is component which sits inside node where such config information can be stored and shared with all the pods within node.

**Secrets**
- Secrets component is similar to configMap which is only used to store secrets and follows encryption way of storing properties

**Deployment**
- To manage availability pods are usually replicated in another node of K8s cluster.
- K8s handles this replica pod creation when given set of instruction on how to create this.
- Deployment component manages these instructions & as a Dev we just provide this deployment script & K8s takes care of replicating pods as an when needed.

**StatefulSet**
- Pod replicas generally are stateless.
- Imagine DB pod, which talks to remote data storage volume which cannot be stateless.
- This needs additional information about synchronizing state between pod & replicas.
- StatefulSet component is used to provide such pod creation blueprint.
- Managing stateful pods is difficult in K8s hence generally avoided.

## K8s Architecture
K8s is Master slave architecture.
### Slaves / Nodes
are worker nodes which hosts pods.
Worker nodes has 

**Container Runtime** (Docker) to manage containers within pods

**Kubelet**: Process responsible for creating new pods on command from Master nodes.
Also assigns node resources requested by pod to it.

**Kube Proxy**: Kube proxy acts like request router, load balancer between multiple replicas of pods. It also routes requests to nearest or same node pod to avoid network latency.

### Master Nodes
Are nodes which controls worker nodes and also manages K8s cluster.

Master nodes again can be replicated on multiple nodes to manage worker nodes and availability.
Master nodes has 4 processes within,

**API Server**: This acts as a gateway to enter Master node. Requests coming from kubectl, K8s UI or other clients pass through this process. Also acts as authentication to avoid requets coming from untrusted clients.

**Key-Value Store / etcd**: This is a remote data storage across master clusters. This acts like a brain to masters which has entire state of worker nodes, their resouce availability etc.

**Scheduler**: Is responsible to schedule pod creation, it identifies appropriate worker node in cluster with less occupancy and assigns task of pod creation to its kubelet.

**Controller Manager**: Is a process responcible to create a new node, add it to existing worker cluster at runtime, monitor pods within all workers and inform scheduler on pod death.


## Local Setup

### Minikube
Minikube always runs in VM or virtual box & needs a hyperviser to be installed on local.
Minikube installs both Master and worker processes on same virtual box.

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

## Kubectl
👷 WORK IN PROGRESS
Kubectl is K8s client / cmd line interface to interact with K8s.

### CRUD
```console
kubectl create
edit
delete
```
### Monitor
```console
get pod
get deployment
get replicaset
```

### Debug
```console
kubectl logs
interactive terminal to container running inside pod
kubectl describe pod
```

👷 WORK IN PROGRESS
