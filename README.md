# Averbis Helm Charts

A Helm chart repository to deploy Averbis applications in your Kubernetes cluster.

## Prerequisites
- A running Kubernetes cluster ([kind](https://kind.sigs.k8s.io/docs/), [k3s](https://k3s.io/), [minikube](https://minikube.sigs.k8s.io/docs/start/), [rancher](https://rancher.com/) or managed Kubernetes like [AWS EKS](https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html) or [Google GKE](https://cloud.google.com/kubernetes-engine))
- Helm 3.x

## Installing Helm
Helm is a package manager for Kubernetes. Helm Charts are packages of pre-configured Kubernetes resources.

To install Helm, refer to the [Helm install guide](https://helm.sh/docs/intro/install/).

## Register Repository and Browse Applications

```bash
helm repo add averbis https://averbis.github.io/helm-charts
helm search repo averbis
```

## Install Applications
For application installation instructions please refer to the application specific documentation located in the [charts directory](charts).