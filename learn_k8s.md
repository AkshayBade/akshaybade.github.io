---
---

# Kubernetes

## Plan 🕙
- [ ]  Prerequisites
    - [ ]  What is container
    - [ ]  Service Discovery
    - [ ]  Networking Basics
- [ ]  What is Kubernetes
- [ ]  K8s Architecture 👎
- [ ]  Local Setup
    - [ ]  Ways of setup
    - [x]  Minikube
    - [ ]  Cluster
- [ ]  Core components
    - [ ]  Kubeconfig
    - [ ]  Objects, Resources
    - [ ]  pods, nodes, services
- [ ]  Kubernetes API
    - [ ]  kubectl
- [ ]  Advance Topics
    - [ ]  Networking
    - [ ]  Storage
    - [ ]  Monitoring
    - [ ]  Workflows

## Index
- [Local Setup](local-setup)


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
