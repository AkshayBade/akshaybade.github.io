---
---

# Kubernetes

## Plan 🕙
- [x]  Prerequisites
    - [x]  What is container
    - [x]  Service Discovery
    - [x]  Networking Basics
- [x]  What is Kubernetes
- [ ]  K8s components
    - [x]  pods, nodes, services
    - [x]  Kubeconfig
    - [ ]  namespaces
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

### Kubeconfig
K8s uses YAML for writing configurations of the processes.
Any configuration file mainly has 3 sections.
- Metadata
- Selector
- Template
**Deployment yaml**
Deployment config provides blueprint for creating pods.

**Service yaml**
Service yaml creates port binding between pod mentioned in deployment.
app label is used to map service to corresponding deployment.

**Ingress yaml**

### Namespaces
**Characteristics**</p>
To group related service pods under common access, resource control namespaces can be used.</p>
If not mentioned pods are created under namespace called `default`.</p>
User access can be controlled at NS level.</p>
Resource allocation like CPU, memory can be contrlled at NS level.</p>
only services can be accessed across namespaces by mentioning service-name.namespace </p>
kinds like configmap need to be created by namespaces</p>

**Usecases**:</p>
Logically group services inside database, monitoring, APIs etc.</p>
Grouping common resoures like DB, services which can be accessed in difference envs.</p>
Blue/Green deployent</p>
Avoid pod overriding: If 2 pods has same name they will override eachother without notice, so team specific NS helps.</p>

```console
kubectl get namespace

kubectl create namespace <NS_NAME>

kubectl apply -f deployment.yaml -n <NS_NAME>

#Mention NS in deployment -> metadata section, if not mentioned assigned default.

kubectl get service -n <NS_NAME>

#We can change active namespace from default to <NS_NAME> to avoid mentioning this in every ctl command.

kubens
```


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
Kubectl is K8s client / cmd line interface to interact with K8s.

### CRUD
```console
# Create new application pod with deployment command
#Below command creates deployment file with default configs
kubectl create deployment my-mongo --image=mongo
kubectl get deployment
kubectl get pod
kubectl get replicaset

# Make changes to that deployment file, like increasing replica from default 1 to 2.
kubectl edit deployment my-mongo
kubectl get replicaset

# delete pod from K8s cluster
kubectl delete deployment my-mongo
```

### Monitor
```console
kubectl get deployment
kubectl get pod
kubectl get replicaset
```

### Debug
```console
# Check logs of pod
kubectl logs <POD_NAME>
# interactive terminal to container running inside pod
kubectl exec -it <POD_NAME> -- bin/bash

# Get more details of pod , service or deployment
kubectl describe <POD/DEP/Service>
```

👷 WORK IN PROGRESS
