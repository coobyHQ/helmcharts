# Odoo base chart

> Odoo base chart provides persistent volumes on OpenEBS for addons and filestore and a single postgres container.

[Odoo](https://www.odoo.com/) is a suite of web-based open source business apps. The main Odoo Apps include an Open Source CRM, Website Builder, eCommerce, Project Management, Billing & Accounting, Point of Sale, Human Resources, Marketing, Manufacturing, Purchase Management, ...

Odoo Apps can be used as stand-alone applications, but they also integrate seamlessly so you get a full-featured Open Source ERP when you install several Apps.

## TL;DR;

```console
$ helm install stable/odoo-base
```

## Introduction

This chart bootstraps a [Odoo](https://github.com/coobyHQ/cooby-docker-odoo-base) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/odoo
```

The command deploys Odoo on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the Odoo chart and their default values.

|               Parameter               |                Description                                  |                   Default                      |
|---------------------------------------|-------------------------------------------------------------|------------------------------------------------|
| `global.imageRegistry`                | Global Docker image registry                                | `nil`                                          |
| `image.registry`                      | Odoo image registry                                         | `docker.io`                                    |
| `image.repository`                    | Odoo Image name                                             | `coobytec/odoo-base`                                 |
| `image.tag`                           | Odoo Image tag                                              | `{VERSION}`                                    |
| `image.pullPolicy`                    | Image pull policy                                           | `Always`                                       |
| `image.pullSecrets`                   | Specify image pull secrets                                  | `nil`                                          |
| `service.type`                        | Kubernetes Service type                                     | `LoadBalancer`                                 |
| `service.port`                        | Service HTTP port                                           | `80`                                          |
| `service.loadBalancer`                | Kubernetes LoadBalancerIP to request                        | `nil`                                          |
| `service.externalTrafficPolicy`       | Enable client source IP preservation                        | `Cluster`                                      |
| `service.nodePort`                    | Kubernetes http node port                                   | `""`                                           |
| `ingress.enabled`                     | Enable ingress controller resource                          | `false`                                        |
| `ingress.hosts[0].name`               | Hostname to your Odoo installation                          | `odoo.local`                                   |
| `ingress.hosts[0].path`               | Path within the url structure                               | `/`                                            |
| `ingress.hosts[0].tls`                | Utilize TLS backend in ingress                              | `false`                                        |
| `ingress.hosts[0].certManager`        | Add annotations for cert-manager                            | `false`                                        |
| `ingress.hosts[0].tlsSecret`          | TLS Secret (certificates)                                   | `odoo.local-tls-secret`                        |
| `ingress.hosts[0].annotations`        | Annotations for this host's ingress record                  | `[]`                                           |
| `ingress.secrets[0].name`             | TLS Secret Name                                             | `nil`                                          |
| `ingress.secrets[0].certificate`      | TLS Secret Certificate                                      | `nil`                                          |
| `ingress.secrets[0].key`              | TLS Secret Key                                              | `nil`                                          |
| `resources`                           | CPU/Memory resource requests/limits                         | Memory: `512Mi`, CPU: `300m`                   |
| `persistence.storageClass`            | PVC Storage Class                                           | `openebs-jiva-default`                         |
| `persistence.accessMode`              | PVC Access Mode                                             | `ReadWriteOnce`                                |
| `persistence.size`                    | PVC Storage Request                                         | `8Gi`                                          |
| `postgresql.postgresqlPassword`       | PostgreSQL password                                         | `nil`                                          |
| `postgresql.persistence.enabled`      | Enable PostgreSQL persistence using PVC                     | `true`                                         |
| `postgresql.persistence.storageClass` | PVC Storage Class for PostgreSQL volume                     | `openebs-jiva-default`                         |
| `postgresql.persistence.accessMode`   | PVC Access Mode for PostgreSQL volume                       | `ReadWriteOnce`                                |
| `postgresql.persistence.size`         | PVC Storage Request for PostgreSQL volume                   | `8Gi`                                          |
| `livenessProbe.enabled`               | Enable/disable the liveness probe                           | `true`                                         |
| `livenessProbe.initialDelaySeconds`   | Delay before liveness probe is initiated                    | 300                                            |
| `livenessProbe.periodSeconds`         | How often to perform the probe                              | 30                                             |
| `livenessProbe.timeoutSeconds`        | When the probe times out                                    | 5                                              |
| `livenessProbe.failureThreshold`      | Minimum consecutive failures to be considered failed        | 6                                              |
| `livenessProbe.successThreshold`      | Minimum consecutive successes to be considered successful   | 1                                              |
| `readinessProbe.enabled`              | Enable/disable the readiness probe                          | `true`                                         |
| `readinessProbe.initialDelaySeconds`  | Delay before readinessProbe is initiated                    | 30                                             |
| `readinessProbe.periodSeconds   `     | How often to perform the probe                              | 10                                             |
| `readinessProbe.timeoutSeconds`       | When the probe times out                                    | 5                                              |
| `readinessProbe.failureThreshold`     | Minimum consecutive failures to be considered failed        | 6                                              |
| `readinessProbe.successThreshold`     | Minimum consecutive successes to be considered successful   | 1                                              |

The above parameters map to the env variables defined in [coobytec/odoo-base](http://github.com/coobyHQ/cooby-docker-odoo-base). For more information please refer to the [coobytec/odoo-base](http://github.com/coobyHQ/cooby-docker-odoo-base) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set odooPassword=password,postgresql.postgresPassword=secretpassword \
    stable/odoo
```

The above command sets the Odoo administrator account password to `password` and the PostgreSQL `postgres` user password to `secretpassword`.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml stable/odoo
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

The [Cooby Odoo](https://github.com/coobyHQ/cooby-docker-odoo-base) image stores the Odoo data and configurations at the `/coobytec/odoo-base` path of the container.

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube.
See the [Configuration](#configuration) section to configure the PVC or to disable persistence.

## Upgrading

### To 3.0.0

Backwards compatibility is not guaranteed unless you modify the labels used on the chart's deployments.
Use the workaround below to upgrade from versions previous to 3.0.0. The following example assumes that the release name is odoo:

```console
$ kubectl patch deployment odoo-odoo --type=json -p='[{"op": "remove", "path": "/spec/selector/matchLabels/chart"}]'
$ kubectl patch deployment odoo-postgresql --type=json -p='[{"op": "remove", "path": "/spec/selector/matchLabels/chart"}]'
```
