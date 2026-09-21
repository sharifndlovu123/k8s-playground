# Small App on minikube

This tutorial shows you how to run a sample app on Kubernetes using minikube. The tutorial provides a container image that uses NGINX to echo back all the requests.

## Prerequisites

- minikube installed (see [minikube guide](../03-local-clusters/minikube.md))
- `kubectl` installed

## 1. Start a cluster

```bash
minikube start
minikube status
```

## 2. Create a Deployment

A Deployment manages a Pod and restarts it if it fails.

```bash
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```

Check that it's running:

```bash
kubectl get deployments
kubectl get pods
```

## 3. Expose it as a Service

By default the Pod is only reachable inside the cluster. Expose it on a `NodePort`:

```bash
kubectl expose deployment hello-minikube --type=NodePort --port=8080
kubectl get services hello-minikube
```

## 4. Open the app

Let minikube open the Service in your browser:

```bash
minikube service hello-minikube
```

Or print the URL and call it yourself:

```bash
minikube service hello-minikube --url
curl <url-from-above>
```

The app echoes back the details of your request.

Alternatively, forward a local port to the Service:

```bash
kubectl port-forward service/hello-minikube 7080:8080
curl http://localhost:7080
```

## 5. Clean up

```bash
kubectl delete service hello-minikube
kubectl delete deployment hello-minikube
minikube stop
```

---

## Declarative approach

Steps 2 and 3 can be replaced by a single manifest, [`hello-minikube.yaml`](hello-minikube.yaml), which declares both the Deployment and the Service (separated by `---`).

```bash
# Create (or update) everything in the file
kubectl apply -f hello-minikube.yaml

kubectl get deployments,services

# Open it (same as step 4)
minikube service hello-minikube
```

Change something (e.g. `replicas: 3`) and re-run `kubectl apply -f hello-minikube.yaml` to update the cluster to match the file.

Clean up everything the file created:

```bash
kubectl delete -f hello-minikube.yaml
```
