# Averbis Tableau Web Data Connector Helm Chart

This chart deploys the Averbis Web Data Connector for Tableau

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
To install the chart with the release name `tableau-connector`:
```
helm install tableau-connector averbis-charts/tableau-connector
```
### Installing using Chart Sources
To install the chart with the release name `tableau-connector` using cloned chart sources:
```
helm install tableau-connector .
```

## Upgrading the Chart
Upgrade the `tableau-connector` release to the latest chart version.
```
helm repo update
helm upgrade tableau-connector averbis-charts/tableau-connector
```

## Uninstalling the Chart
Uninstall the `tableau-connector` release. This will delete all Kubernetes components associated with this chart.

```
helm uninstall tableau-connector
```
