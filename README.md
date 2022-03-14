<!--- app-name: swe-api -->

# Spring Web Essentials API Helm Chart

__Description:__ A Helm chart for the Spring Web Essentials API

                           
## TL;DR

Add the repo:
```console
helm repo add jeffs-charts https://jeffrey-anderson.github.io/helm-charts/
```

Install the chart and the [database](https://github.com/jeffrey-anderson/swe-db-helm-chart):
```console
helm install my-api-release jeffs-charts/swe-api
```

Install the chart and use an externally provided PostgreSQL database:
```console
helm install my-api-release jeffs-charts/swe-api --set installSweDb=false --set dbUrl=jdbc:postgresql://<some-db-server-address>:5432/postgres
```

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure
- ReadWriteMany volumes for deployment scaling

## Installing the Chart

To install the chart with the release name `my-api-release`:

```console
helm install my-api-release jeffs-charts/swe-api
```


## Uninstalling the Chart

To uninstall/delete the `my-api-release` deployment:

```console
helm delete my-api-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.


## Commonly Overridden Parameters

| Name                      | Description                                     | Default Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `installSweDb` | True to install the `swe-db` database dependency | `true` |
| `dbSecretName` | The name of the secret that contains the database password | `"postgres-db-password"` |
| `dbUrl` | The database connection URL | No default value. Must be provided if `installSweDb` is `true`, ignored otherwise. |
| `service.type` | How the API is exposed | `LoadBalancer` |
| `service.port` | The port external clients can use to invoke the API | 3000 |

See the full list of parameters in [values.yaml](values.yaml)..

## Commonly Overridden swe-db Parameters

| Name                      | Description                                     | Default Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `swe-db.secret.postgresDbPassword` | base64 encoded password for the database | `VXNlLWEtQmV0dGVyLVBhc3N3MHJk` which decodes to "Use-a-Better-Passw0rd"
| `swe-db.initContainers.runInit` | Toggle init processing | `false` |
| `swe-db.initCommand` | Command to run when initializing the database | "wget -q -O /sql/init-swe-db.sh https://raw.githubusercontent.com/jeffrey-anderson/intro-to-kubernetes/main/swe/init-swe-db.sh 2> /dev/null" |
| `swe-db.service.type` | How the database is exposed | `NodePort` |
| `swe-db.service.nodePort` | Cluster node port port where the database is listening | 30432 |

See the [swe-db README](https://github.com/jeffrey-anderson/swe-db-helm-chart/blob/master/README.md) for more. 

### Overriding via the Command Line

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example, to install the chart and prepopulate the database with some sample data:

```console
helm install my-api-release jeffs-charts/swe-api --set swe-db.initContainers.runInit=true
```

### Overriding via a YAML File

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install my-api-release -f values.yaml jeffs-charts/swe-api
```

> **Tip**: You can use the default [values.yaml](values.yaml).

