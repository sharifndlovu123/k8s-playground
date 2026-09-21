# Resource Kinds and API Versions

Every manifest starts with two fields that say *what* it is:

```yaml
apiVersion: apps/v1   # which API group and version the resource belongs to
kind: Deployment      # the resource type
```

This page is a quick reference for the `kind` values you'll meet in docs and manifests. It's a draft to grow as the learning goes on.

## Contents

- [Reading apiVersion](#reading-apiversion)
- [Workloads](#workloads)
- [Networking](#networking)
- [Configuration and storage](#configuration-and-storage)
- [Cluster organisation and access](#cluster-organisation-and-access)
- [How many kinds are there?](#how-many-kinds-are-there)
- [Commands for exploring](#commands-for-exploring)

## Reading apiVersion

- `v1` is the **core** group (Pod, Service, ConfigMap, ...).
- `<group>/<version>` is a **named** group, e.g. `apps/v1`, `batch/v1`, `networking.k8s.io/v1`.
- Versions signal maturity: `v1` is stable, `v1beta1` is still changing, `v1alpha1` is experimental.
- The same kind can move groups or versions between Kubernetes releases, so always check the docs for your cluster version.

## Workloads

| Kind | apiVersion | Purpose |
|---|---|---|
| **Pod** | `v1` | Smallest unit: one or more containers sharing network and storage |
| **ReplicaSet** | `apps/v1` | Keeps N identical Pods running (you rarely create these directly) |
| **Deployment** | `apps/v1` | Manages ReplicaSets, giving rolling updates and rollbacks (the usual choice for stateless apps) |
| **StatefulSet** | `apps/v1` | Pods with stable names and storage, for databases and similar |
| **DaemonSet** | `apps/v1` | One Pod per node, for log collectors and monitoring agents |
| **Job** | `batch/v1` | Run a task to completion |
| **CronJob** | `batch/v1` | A Job on a schedule |

## Networking

| Kind | apiVersion | Purpose |
|---|---|---|
| **Service** | `v1` | Stable address and load balancing for Pods (`ClusterIP`, `NodePort`, `LoadBalancer`) |
| **Ingress** | `networking.k8s.io/v1` | HTTP/HTTPS routing into the cluster |
| **NetworkPolicy** | `networking.k8s.io/v1` | Firewall rules between Pods |

## Configuration and storage

| Kind | apiVersion | Purpose |
|---|---|---|
| **ConfigMap** | `v1` | Non-secret config |
| **Secret** | `v1` | Passwords, tokens, keys |
| **PersistentVolume** | `v1` | A piece of storage in the cluster |
| **PersistentVolumeClaim** | `v1` | A Pod's request for storage |
| **StorageClass** | `storage.k8s.io/v1` | Defines how volumes are provisioned dynamically |

## Cluster organisation and access

| Kind | apiVersion | Purpose |
|---|---|---|
| **Namespace** | `v1` | Logical partition of the cluster |
| **ServiceAccount** | `v1` | Identity for Pods |
| **Role / ClusterRole** | `rbac.authorization.k8s.io/v1` | Permissions (namespace-wide or cluster-wide) |
| **RoleBinding / ClusterRoleBinding** | `rbac.authorization.k8s.io/v1` | Grant those permissions to users or accounts |
| **ResourceQuota / LimitRange** | `v1` | Cap resource usage |
| **HorizontalPodAutoscaler** | `autoscaling/v2` | Scale replicas based on load |

## How many kinds are there?

- **Built-in:** roughly 60 to 80 resource types on a fresh cluster, depending on the Kubernetes version. Only around 15 to 20 cover most day-to-day work: Pod, Deployment, Service, ConfigMap, Secret, Ingress, Namespace, the storage and RBAC kinds, and Jobs.
- **Custom:** **CRDs** (CustomResourceDefinitions) let tools add their own kinds, e.g. Prometheus, cert-manager, Istio and Argo resources. A cluster with several of these can easily reach hundreds, so there's no fixed total.

## Commands for exploring

```bash
# Every resource type your cluster knows, with its group and kind
kubectl api-resources

# Just one group
kubectl api-resources --api-group=apps

# The apiVersion values available on the cluster
kubectl api-versions

# Docs for a kind and its fields
kubectl explain deployment
kubectl explain deployment.spec
```

> **Tip:** `kubectl explain` shows the `apiVersion` and every field for the version your cluster runs, so it's the fastest way to check a doc example against reality.
