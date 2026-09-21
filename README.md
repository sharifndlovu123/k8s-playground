# Kubernetes Notes

Personal study notes on running and understanding Kubernetes. The folders are numbered in the order they're meant to be read.

## Structure

```
kubernetes/
├── 01-getting-started/
│   └── playgrounds.md
├── 02-concepts/
│   ├── kubectl.md
│   ├── cluster-architecture.md
│   └── images/
├── 03-local-clusters/
│   ├── minikube.md
│   ├── kind.md
│   └── images/
├── 04-sample-app/
│   ├── README.md
│   └── hello-minikube.yaml
└── 05-production/
    └── production-grade-clusters.md
```

## Index

| # | Folder | Notes | What's inside |
|---|---|---|---|
| 1 | Getting started | [playgrounds](01-getting-started/playgrounds.md) | Free browser-based Kubernetes sandboxes, no setup |
| 2 | Concepts | [kubectl](02-concepts/kubectl.md) | Imperative vs declarative `kubectl` |
| | | [cluster architecture](02-concepts/cluster-architecture.md) | Single-node → multi-master topologies, etcd/Raft, component cheat sheet |
| 3 | Local clusters | [minikube](03-local-clusters/minikube.md) | Setup, multi-node, HA and profiles |
| | | [kind](03-local-clusters/kind.md) | Kubernetes IN Docker: setup and multi-node configs |
| 4 | Sample app | [README](04-sample-app/README.md) | NGINX echo app on minikube, imperative and declarative ([manifest](04-sample-app/hello-minikube.yaml)) |
| 5 | Production | [production-grade clusters](05-production/production-grade-clusters.md) | Managed services, distributions, tooling, on-prem challenges |
