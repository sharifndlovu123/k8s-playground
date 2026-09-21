# Kubernetes Notes

Personal study notes on running and understanding Kubernetes.

## Index

| Section | What's inside |
|---|---|
| [playground.md](playground.md) | Free browser-based Kubernetes sandboxes |
| [extra/1.kubectl.md](extra/1.kubectl.md) | Imperative vs declarative `kubectl` |
| [extra/2.highly-available.md](extra/2.highly-available.md) | Single-node → multi-master topologies, etcd/Raft, component cheat sheet |
| [minikube-tutorial/samples.md](minikube-tutorial/samples.md) | minikube setup, multi-node, HA and profiles |
| [kind-tutorial/samples.md](kind-tutorial/samples.md) | kind (Kubernetes IN Docker) setup and multi-node configs |
| [small-app-minikube/README.md](small-app-minikube/README.md) | Sample NGINX app on minikube *(stub)* |
| [MUST-KNOWS/production-grade-clusters.md](MUST-KNOWS/production-grade-clusters.md) | Managed services, distributions, tooling, on-prem challenges |

## Suggested reading order

1. [Playgrounds](playground.md): try Kubernetes with zero setup
2. [kubectl](extra/1.kubectl.md): learn how you talk to a cluster
3. [Topologies and HA](extra/2.highly-available.md): learn how clusters are built
4. [minikube](minikube-tutorial/samples.md) and [kind](kind-tutorial/samples.md): run one locally
5. [Production-grade clusters](MUST-KNOWS/production-grade-clusters.md): what "real" looks like
