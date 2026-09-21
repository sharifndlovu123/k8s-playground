# kubectl: Imperative vs Declarative

`kubectl` supports two styles of syntax: **imperative** and **declarative**.

## Imperative syntax

You issue commands that directly modify the state of the cluster, based on the arguments and parameters passed to the `kubectl` command.

```bash
# Create a pod called my-pod, based on the busybox:latest container image
kubectl run my-pod --restart Never --image busybox:latest

# List all ReplicaSet resources in the my-namespace namespace
kubectl get rs -n my-namespace

# Delete a pod called my-pod in the default namespace
kubectl delete pods my-pod
```

It is the easiest style and it's fast. But it is difficult to keep track of, and to remember, all the imperative commands needed to bring a cluster to the state you want. Hence the declarative syntax.

## Declarative syntax

You declare **what you want**, and Kubernetes creates it. Use JSON or YAML (YAML is preferred).

It makes it easy to define configs for resources such as Deployments, Services and Pods, and it supports:

- version control
- collaboration
- repeatability

The imperative example from before:

```bash
kubectl run my-pod --restart Never --image busybox:latest
```

The declarative equivalent:

```yaml
apiVersion: v1                      # API version the resource is declared in; Pod is v1
kind: Pod                           # resource type
metadata:                           # extra data about the resource
  name: my-pod                      # name of the resource
spec:                               # tells k8s what the object is made of
  containers:
    - name: busybox-container       # name of the container
      image: busybox:latest
```

To create the pod, run:

```bash
kubectl create -f filename.yaml
```

### Example: multiple resources in one file

Separate resources with `---`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
    - name: busybox-container
      image: busybox:latest
---
apiVersion: v1
kind: Pod
metadata:
  name: my-second-pod
spec:
  containers:
    - name: nginx-container
      image: nginx:latest
```

> 💡 Run `kubectl explain --help` for documentation.

> **NB:** Remember to learn both. Not all features are available with the imperative approach or the declarative one, so using both is important for closing those gaps.

## Where to run kubectl from

`kubectl` is not always a requirement, but for large projects it is advised. You can use your local machine or a server to access the Kubernetes cluster directly, but don't do it.

If you're looking to automate maintenance or deployment tasks against the cluster, use CI tools such as GitLab CI, Tekton or Jenkins. This requires the CI agents to have:

- `kubectl` installed
- properly configured `kubeconfig` files written to the agent's file system
