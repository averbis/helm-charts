# Patent Monitor Helm Chart

This chart deploys Patent Monitor in your Kubernetes cluster.

## Prerequisites

- A running Kubernetes cluster
- Persistent volume provisioner support in the underlying Kubernetes infrastructure
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
```

## Installing the Chart

The chart can be installed using the helm repository or by checking out the chart sources.

### Installing using Helm Repository
To install the chart with the release name `pm`:

```
helm install pm averbis/patent-monitor
```

### Installing using Chart Sources
To install the chart with the release name `pm` using cloned chart sources:
```
helm install pm .
```

### Chart Parameters
The chart can optionally be configured using the following parameters:

| Name        | Description         | Default Value     |
| :----------:|:-------------------:| :----------------:|
| `maxMemory` | Maximum memory      | 16G               |
| `existingDbSecret`  | Use MariaDB credentials from an existing secret. The secret has to contain the keys `databaseRootPassword`, `databasePassword` and `databaseUsername` | "" |
| `externalDbConnectionUrl` | JDBC connection URL of an external MariaDB 10.x database. Requires the `existingDbSecret` parameter to be set | "" |


Specify each parameter using the `--set name=value` argument to `helm install` and `helm upgrade`  to overwrite the chart default values, for example:

```
helm install pm averbis/patent-monitor --set maxMemory=24G,existingDbSecret=my-secret,externalDbConnectionUrl=jdbc:mariadb://my-mariadb-host:3306/mydb?useMysqlMetadata=true
```

NOTE: Once this chart is deployed, it is not possible to change the MariaDB access credentials, such as usernames or passwords, using Helm.


### Exposing the Application
Create a kubernetes `service` of type `loadBalancer` to access the application from outside the kubernetes cluster. Out of the box this only works
with cloud providers like Google GKE or AWS EKS.

```
kubectl expose deployment patent-monitor --type=LoadBalancer --name=pm-load-balancer
```

Determine the load balancer URL:
```
kubectl get service

NAME                       TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)          AGE
database                   ClusterIP      10.3.243.52    <none>         3306/TCP         9m30s
gcm                        ClusterIP      10.3.247.190   <none>         8181/TCP         9m30s
pm-load-balancer           LoadBalancer   10.3.249.243   34.91.59.210   8080:30790/TCP   6m2s
patent-monitor             ClusterIP      10.3.246.164   <none>         8080/TCP         9m30s
kubernetes                 ClusterIP      10.3.240.1     <none>         443/TCP          21m
solr                       ClusterIP      10.3.253.18    <none>         8983/TCP         9m30s
```

You can access the application using the `EXTERNAL-IP` of the `pm-load-balancer` service at http://EXTERNAL-IP:8080/patent-monitor


## Upgrading the Chart
Upgrade the `pm` release to the latest chart version. Data and configuration settings will be migrated.
```
helm repo update
helm upgrade pm averbis/patent-monitor
```

## Uninstalling the Chart
Uninstall the `pm` release. This will delete all Kubernetes components associated with this chart. All data and configuration settings will be deleted as well.

```
helm uninstall pm
```