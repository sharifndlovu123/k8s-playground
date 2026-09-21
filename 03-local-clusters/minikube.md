# minikube

## Contents

- [Installation](#installation)
- [Configuration](#configuration)
- [Starting a cluster](#starting-a-cluster)
- [Checking the cluster](#checking-the-cluster)
- [Stopping, pausing and deleting](#stopping-pausing-and-deleting)
- [Multi-node cluster](#multi-node-cluster)
- [Multi-master (HA) cluster](#multi-master-ha-cluster)
- [Multiple clusters with profiles](#multiple-clusters-with-profiles)

## Installation

```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Verify the minikube command and path
which minikube
# /usr/local/bin/minikube
```

## Configuration

Set defaults for resources, runtime and driver:

```bash
minikube config set cpus 4
minikube config set memory 16000
minikube config set container-runtime containerd

minikube config set driver docker
# or set VirtualBox as the driver
minikube config set driver virtualbox
```

Each command prints:

```text
❗  These changes will take effect upon a minikube delete and then a minikube start
```

View a setting:

```bash
minikube config view driver
# - driver: docker
```

## Starting a cluster

Start with a specific Kubernetes version:

```bash
minikube start --driver=virtualbox --memory=8000m --cpus=2 --kubernetes-version=1.29.0
```

## Checking the cluster

Cluster status:

```bash
minikube status
```

By default, the kubectl configuration lives in `~/.kube/config`:

```bash
kubectl config view
```

Show which Kubernetes cluster your kubectl is pointing to:

```bash
kubectl config current-context
```

Check the control plane components:

```bash
kubectl get componentstatuses
```

```text
Warning: v1 ComponentStatus is deprecated in v1.19+
NAME                 STATUS    MESSAGE   ERROR
controller-manager   Healthy   ok
scheduler            Healthy   ok
etcd-0               Healthy   ok
```

## Stopping, pausing and deleting

Stop the local minikube cluster:

```bash
minikube stop
minikube status
```

Or pause it to allow a quick startup later:

```bash
minikube pause
minikube unpause
```

## Multi-node cluster

> **NB:** Make sure your workstation has enough resources to create multiple Kubernetes nodes (VMs or containers). minikube spins up every node with the same vCPU and memory given in settings or arguments.

```bash
minikube start --driver=podman --nodes=3
kubectl get nodes
```

The first node is the control plane (master) node, and the remaining two are compute nodes.

## Multi-master (HA) cluster

```bash
minikube start \
  --driver=virtualbox \
  --nodes 5 \
  --ha true \
  --cni calico \
  --cpus=2 \
  --memory=2g \
  --kubernetes-version=v1.30.0 \
  --container-runtime=containerd

kubectl get nodes
```

```text
NAME           STATUS   ROLES           AGE     VERSION
minikube       Ready    control-plane   6m28s   v1.30.0
minikube-m02   Ready    control-plane   4m36s   v1.30.0
minikube-m03   Ready    control-plane   2m45s   v1.30.0
minikube-m04   Ready    <none>          112s    v1.30.0
minikube-m05   Ready    <none>          62s     v1.30.0
```

minikube creates a five-node cluster (`--nodes 5`) and configures the first three nodes as control plane nodes (`--ha true`).

## Multiple clusters with profiles

Simulate an environment with multiple Kubernetes clusters:

```bash
# Start a cluster using VirtualBox as the driver
minikube start --driver=virtualbox --kubernetes-version=1.30.0 --profile cluster-vbox

# Start another cluster using Docker as the driver
minikube start --driver=docker --kubernetes-version=1.30.0 --profile cluster-docker

minikube profile list
```

To stop, delete, etc., use `--profile`:

```bash
# Stop a cluster by profile name
minikube stop --profile cluster-docker

# Remove a cluster by profile name
minikube delete --profile cluster-docker
```
