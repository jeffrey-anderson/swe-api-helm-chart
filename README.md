<!--- app-name: swe-api -->

# Spring Web Essentials API Helm Chart

__Description:__ A Helm chart for the Spring Web Essentials API

                           
## TL;DR

```console
helm repo add jeffs-charts https://jeffrey-anderson.github.io/helm-charts/

helm install audacious-apple jeffs-charts/swe-api
```

## Prerequisites

- Kubernetes 1.19+
- Helm 3.2.0+
- PV provisioner support in the underlying infrastructure
- ReadWriteMany volumes for deployment scaling

## Installing the Chart

To install the chart with the release name `audacious-apple`:

```console
helm install audacious-apple jeffs-charts/swe-api
```


## Uninstalling the Chart

To uninstall/delete the `audacious-apple` deployment:

```console
helm delete audacious-apple
```

The command removes all the Kubernetes components associated with the chart and deletes the release.


## Commonly Overridden Parameters

| Name                      | Description                                     | Default Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `dbSecretName` | The name of the secret that contains the database password | `"postgres-db-password"` |
| `dbUrl` | The database connection URL | `jdbc:postgresql://perky-porcupine-swe-db:5432/postgres` |
| `service.type` | How the API is exposed | `LoadBalancer` |
| `service.port` | The port external clients can use to invoke the API | 3000 |

For a complete list of parameters, you can override, see [values.yaml](values.yaml)

### Overriding via the Command Line

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install audacious-apple --set dbUrl=jdbc:postgresql://another-release-swe-db:5432/postgres jeffs-charts/swe-api
```

### Overriding via a YAML File

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install audacious-apple -f values.yaml jeffs-charts/swe-api
```

> **Tip**: You can use the default [values.yaml](values.yaml).

