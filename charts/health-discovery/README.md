# Health Discovery Helm Chart

This chart deploys Health Discovery in your Kubernetes cluster.

## Prerequisites

- A running Kubernetes cluster with at least 24 GB Ram on each worker node
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
helm repo add averbis https://averbis.github.io/helm-charts/
helm repo update
```

## Installing the Chart

The chart can be installed using the helm repository or by checking out the chart sources.

### Installing using Helm Repository
```
helm install hd averbis/health-discovery
```
### Installing using Chart Sources
```
helm install hd .
```

### Exposing the Application
Create a kubernetes `service` of type `loadBalancer` to access the application from outside the kubernetes cluster. Out of the box this only works
with cloud providers like Google GKE or AWS EKS.

```
kubectl expose deployment health-discovery-hd --type=LoadBalancer --name=hd-load-balancer
```

Determine the load balancer URL:
```
kubectl get service

NAME                       TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
database                   ClusterIP      10.3.243.52    <none>         3306/TCP         9m30s
gcm                        ClusterIP      10.3.247.190   <none>         8181/TCP         9m30s
hd-load-balancer           LoadBalancer   10.3.249.243   34.91.59.210   8080:30790/TCP   6m2s
health-discovery-hd        ClusterIP      10.3.246.164   <none>         8080/TCP         9m30s
kubernetes                 ClusterIP      10.3.240.1     <none>         443/TCP          21m
solr                       ClusterIP      10.3.253.18    <none>         8983/TCP         9m30s
```

You can access the application using the `EXTERNAL-IP` of the `health-discovery-hd` service at http://EXTERNAL-IP:8080/health-discovery


## Upgrading the Chart
```
 helm upgrade hd averbis/health-discovery
```

## Uninstalling the Chart
```
helm uninstall hd
```
