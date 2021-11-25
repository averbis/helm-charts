# Averbis Kafka Helm Chart

This chart deploys Averbis Kafka in your Kubernetes cluster.

## Prerequisites

- A running Kubernetes cluster
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Helm](https://helm.sh/docs/intro/install/)

## Creating Secret to pull Images

Create a secret named `averbis-docker-registry` with your Averbis credentials to pull images from the [Averbis docker registry](https://registry.averbis.com):

```
kubectl create secret docker-registry averbis-docker-registry \
--docker-server=https://registry.averbis.com \
--docker-username=me@example.com \
--docker-password=MySecretPassword
```

## Adding the Helm Repository
```
helm repo add averbis-charts https://averbis.github.io/helm-charts/
```

## Installing the Chart

The chart can be installed using the helm repository or by checking out the chart sources.

### Installing using Helm Repository
To install the chart with the release name `kafka`:
```
helm install kafka averbis-charts/kafka
```
### Installing using Chart Sources
To install the chart with the release name `kafka` using cloned chart sources:
```
helm install kafka .
```

## Upgrading the Chart
Upgrade the `kafka` release to the latest chart version.
```
helm repo update
helm upgrade kafka averbis-charts/kafka
```

## Uninstalling the Chart
To uninstall the `kafka` release. This will delete all Kubernetes components associated with this chart. All data and configuration settings will be deleted as well.

```
helm uninstall kafka
```
