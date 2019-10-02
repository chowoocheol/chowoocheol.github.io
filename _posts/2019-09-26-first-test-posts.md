---
title: First Test Posts
---

> 첫번째

# 하하
http://www.nfvd.kr:3000/projects/nfvd-nfvo/issues?query_id=138

![Screenshot_3](https://user-images.githubusercontent.com/15685081/66021204-cba9d880-e524-11e9-8d17-aaca7528871f.png)


# MariaDB

[MariaDB](https://mariadb.org) is one of the most popular database servers in the world. It’s made by the original developers of MySQL and guaranteed to stay open source. Notable users include Wikipedia, Facebook and Google.

MariaDB is developed as open source software and as a relational database it provides an SQL interface for accessing data. The latest versions of MariaDB also include GIS and JSON features.

## TL;DR

```bash
$ helm install stable/mariadb
```

## Introduction

This chart bootstraps a [MariaDB](https://github.com/bitnami/bitnami-docker-mariadb) replication cluster deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This chart has been tested to work with NGINX Ingress, cert-manager, fluentd and Prometheus on top of the [BKPR](https://kubeprod.io/).

## Prerequisites

- Kubernetes 1.10+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release stable/mariadb
```

The command deploys MariaDB on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the MariaDB chart and their default values.

|             Parameter                     |                     Description                     |                              Default                              |
|-------------------------------------------|-----------------------------------------------------|-------------------------------------------------------------------|
| `global.imageRegistry`                    | Global Docker image registry                        | `nil`                                                             |
| `global.imagePullSecrets`                 | Global Docker registry secret names as an array     | `[]` (does not add image pull secrets to deployed pods)           |
| `global.storageClass`                     | Global storage class for dynamic provisioning                                               | `nil`                                                        |
| `image.registry`                          | MariaDB image registry                              | `docker.io`                                                       |
| `image.repository`                        | MariaDB Image name                                  | `bitnami/mariadb`                                                 |
| `image.tag`                               | MariaDB Image tag                                   | `{TAG_NAME}`                                                      |
| `image.pullPolicy`                        | MariaDB image pull policy                           | `IfNotPresent`                                                    |
| `image.pullSecrets`                       | Specify docker-registry secret names as an array    | `[]` (does not add image pull secrets to deployed pods)           |
| `image.debug`                             | Specify if debug logs should be enabled             | `false`                                                           |
| `nameOverride`                            | String to partially override mariadb.fullname template with a string (will prepend the release name) | `nil`            |
| `fullnameOverride`                        | String to fully override mariadb.fullname template with a string                                     | `nil`            |
| `volumePermissions.enabled`          | Enable init container that changes volume permissions in the data directory (for cases where the default k8s `runAsUser` and `fsUser` values do not work) | `false`                                                      |
| `volumePermissions.image.registry`   | Init container volume-permissions image registry                                                                                                          | `docker.io`                                                  |
| `volumePermissions.image.repository` | Init container volume-permissions image name                                                                                                              | `bitnami/minideb`                                            |
| `volumePermissions.image.tag`        | Init container volume-permissions image tag                                                                                                               | `stretch`                                                     |
| `volumePermissions.image.pullPolicy` | Init container volume-permissions image pull policy                                                                                                       | `Always`                                                     |
| `volumePermissions.resources`        | Init container resource requests/limit                                                                                                                    | `nil`                                                        |
| `service.type`                            | Kubernetes service type                             | `ClusterIP`                                                       |
| `service.clusterIp.master`                | Specific cluster IP for master when service type is cluster IP. Use None for headless service | `nil`                   |
| `service.clusterIp.slave`                 | Specific cluster IP for slave when service type is cluster IP. Use None for headless service | `nil`                    |
| `service.port`                            | MySQL service port                                  | `3306`                                                            |
| `serviceAccount.create`                   | Specifies whether a ServiceAccount should be created | `false`                                                          |
| `serviceAccount.name`                     | The name of the ServiceAccount to create            | Generated using the mariadb.fullname template                     |
| `schedulerName`                           | Name of the k8s scheduler (other than default)      | `nil`                                                             |
| `rbac.create`                             | Create and use RBAC resources                       | `false`                                                           |
| `securityContext.enabled`                 | Enable security context                             | `true`                                                            |
| `securityContext.fsGroup`                 | Group ID for the container                          | `1001`                                                            |
| `securityContext.runAsUser`               | User ID for the container                           | `1001`                                                            |
| `existingSecret`                          | Use existing secret for password details (`rootUser.password`, `db.password`, `replication.password` will be ignored and picked up from this secret). The secret has to contain the keys `mariadb-root-password`, `mariadb-replication-password` and `mariadb-password`. |                         |
| `rootUser.password`                       | Password for the `root` user. Ignored if existing secret is provided. | _random 10 character alphanumeric string_       |
| `rootUser.forcePassword`                  | Force users to specify a password                   | `false`                                                           |
| `db.user`                                 | Username of new user to create                      | `nil`                                                             |
| `db.password`                             | Password for the new user. Ignored if existing secret is provided.    | _random 10 character alphanumeric string if `db.user` is defined_ |
| `db.forcePassword`                        | Force users to specify a password                   | `false`                                                           |
| `db.name`                                 | Name for new database to create                     | `my_database`                                                     |
| `replication.enabled`                     | MariaDB replication enabled                         | `true`                                                            |
| `replication.user`                        |MariaDB replication user                             | `replicator`                                                      |
| `replication.password`                    | MariaDB replication user password. Ignored if existing secret is provided. | _random 10 character alphanumeric string_  |
| `replication.forcePassword`               | Force users to specify a password                   | `false`                                                           |
| `initdbScripts`                           | Dictionary of initdb scripts                        | `nil`                                                             |
| `initdbScriptsConfigMap`                  | ConfigMap with the initdb scripts (Note: Overrides `initdbScripts`) | `nil`                                             |
| `master.annotations[].key`                | key for the the annotation list item                |  `nil`                                                            |
| `master.annotations[].value`              | value for the the annotation list item              |  `nil`                                                            |
| `master.extraFlags`                       | MariaDB master additional command line flags        |  `nil`                                                            |
| `master.affinity`                         | Master affinity (in addition to master.antiAffinity when set)  | `{}`                                                   |
| `master.antiAffinity`                     | Master pod anti-affinity policy                     | `soft`                                                            |
| `master.nodeSelector`                     | Master node labels for pod assignment               | `{}`                                                              |
| `master.tolerations`                      | List of node taints to tolerate (master)            | `[]`                                                              |
| `master.updateStrategy`                   | Master statefulset update strategy policy           | `RollingUpdate`                                                   |
| `master.persistence.enabled`              | Enable persistence using PVC                        | `true`                                                            |
| `master.persistence.existingClaim`        | Provide an existing `PersistentVolumeClaim`         | `nil`                                                             |
| `master.persistence.subPath`              | Subdirectory of the volume to mount                 | `nil`                                                             |
| `master.persistence.mountPath`            | Path to mount the volume at                         | `/bitnami/mariadb`                                                |
| `master.persistence.annotations`          | Persistent Volume Claim annotations                 | `{}`                                                              |
| `master.persistence.storageClass`         | Persistent Volume Storage Class                     | ``                                                                |
| `master.persistence.accessModes`          | Persistent Volume Access Modes                      | `[ReadWriteOnce]`                                                 |
| `master.persistence.size`                 | Persistent Volume Size                              | `8Gi`                                                             |
| `master.extraInitContainers`              | Additional init containers as a string to be passed to the `tpl` function (master) |                                    |
| `master.config`                           | Config file for the MariaDB Master server           | `_default values in the values.yaml file_`                        |
| `master.resources`                        | CPU/Memory resource requests/limits for master node | `{}`                                                              |
| `master.livenessProbe.enabled`            | Turn on and off liveness probe (master)             | `true`                                                            |
| `master.livenessProbe.initialDelaySeconds`| Delay before liveness probe is initiated (master)   | `120`                                                             |
| `master.livenessProbe.periodSeconds`      | How often to perform the probe (master)             | `10`                                                              |
| `master.livenessProbe.timeoutSeconds`     | When the probe times out (master)                   | `1`                                                               |
| `master.livenessProbe.successThreshold`   | Minimum consecutive successes for the probe (master)| `1`                                                               |
| `master.livenessProbe.failureThreshold`   | Minimum consecutive failures for the probe (master) | `3`                                                               |
| `master.readinessProbe.enabled`           | Turn on and off readiness probe (master)            | `true`                                                            |
| `master.readinessProbe.initialDelaySeconds`| Delay before readiness probe is initiated (master) | `30`                                                              |
| `master.readinessProbe.periodSeconds`     | How often to perform the probe (master)             | `10`                                                              |
| `master.readinessProbe.timeoutSeconds`    | When the probe times out (master)                   | `1`                                                               |
| `master.readinessProbe.successThreshold`  | Minimum consecutive successes for the probe (master)| `1`                                                               |
| `master.readinessProbe.failureThreshold`  | Minimum consecutive failures for the probe (master) | `3`                                                               |
| `master.podDisruptionBudget.enabled`      | If true, create a pod disruption budget for master pods. | `false`                                                      |
| `master.podDisruptionBudget.minAvailable` | Minimum number / percentage of pods that should remain scheduled | `1`                                                  |
| `master.podDisruptionBudget.maxUnavailable`| Maximum number / percentage of pods that may be made unavailable | `nil`                                               |
| `master.service.annotations`              | Master service annotations                          | `{}`                                                              |
| `slave.replicas`                          | Desired number of slave replicas                    | `1`                                                               |
| `slave.annotations[].key`                 | key for the the annotation list item                | `nil`                                                             |
| `slave.annotations[].value`               | value for the the annotation list item              | `nil`                                                             |
| `slave.extraFlags`                        | MariaDB slave additional command line flags         | `nil`                                                             |
| `slave.affinity`                          | Slave affinity (in addition to slave.antiAffinity when set) | `{}`                                                      |
| `slave.antiAffinity`                      | Slave pod anti-affinity policy                      | `soft`                                                            |
| `slave.nodeSelector`                      | Slave node labels for pod assignment                | `{}`                                                              |
| `slave.tolerations`                       | List of node taints to tolerate for (slave)         | `[]`                                                              |
| `slave.updateStrategy`                    | Slave statefulset update strategy policy            | `RollingUpdate`                                                   |
| `slave.persistence.enabled`               | Enable persistence using a `PersistentVolumeClaim`  | `true`                                                            |
| `slave.persistence.annotations`           | Persistent Volume Claim annotations                 | `{}`                                                              |
| `slave.persistence.storageClass`          | Persistent Volume Storage Class                     | ``                                                                |
| `slave.persistence.accessModes`           | Persistent Volume Access Modes                      | `[ReadWriteOnce]`                                                 |
| `slave.persistence.size`                  | Persistent Volume Size                              | `8Gi`                                                             |
| `slave.extraInitContainers`               | Additional init containers as a string to be passed to the `tpl` function (slave)               |                       |
| `slave.config`                            | Config file for the MariaDB Slave replicas          | `_default values in the values.yaml file_`                        |
| `slave.resources`                         | CPU/Memory resource requests/limits for slave node  | `{}`                                                              |
| `slave.livenessProbe.enabled`             | Turn on and off liveness probe (slave)              | `true`                                                            |
| `slave.livenessProbe.initialDelaySeconds` | Delay before liveness probe is initiated (slave)    | `120`                                                             |
| `slave.livenessProbe.periodSeconds`       | How often to perform the probe (slave)              | `10`                                                              |
| `slave.livenessProbe.timeoutSeconds`      | When the probe times out (slave)                    | `1`                                                               |
| `slave.livenessProbe.successThreshold`    | Minimum consecutive successes for the probe (slave) | `1`                                                               |
| `slave.livenessProbe.failureThreshold`    | Minimum consecutive failures for the probe (slave)  | `3`                                                               |
| `slave.readinessProbe.enabled`            | Turn on and off readiness probe (slave)             | `true`                                                            |
| `slave.readinessProbe.initialDelaySeconds`| Delay before readiness probe is initiated (slave)   | `45`                                                              |
| `slave.readinessProbe.periodSeconds`      | How often to perform the probe (slave)              | `10`                                                              |
| `slave.readinessProbe.timeoutSeconds`     | When the probe times out (slave)                    | `1`                                                               |
| `slave.readinessProbe.successThreshold`   | Minimum consecutive successes for the probe (slave) | `1`                                                               |
| `slave.readinessProbe.failureThreshold`   | Minimum consecutive failures for the probe (slave)  | `3`                                                               |
| `slave.podDisruptionBudget.enabled`       | If true, create a pod disruption budget for slave pods. | `false`                                                       |
| `slave.podDisruptionBudget.minAvailable`  | Minimum number / percentage of pods that should remain scheduled | `1`                                                  |
| `slave.podDisruptionBudget.maxUnavailable`| Maximum number / percentage of pods that may be made unavailable | `nil`                                                |
| `slave.service.annotations`               | Slave service annotations                           | `{}`                                                              |
| `metrics.enabled`                         | Start a side-car prometheus exporter                | `false`                                                           |
| `metrics.image.registry`                  | Exporter image registry                             | `docker.io`                                                       |
| `metrics.image.repository`                | Exporter image name                                 | `bitnami/mysqld-exporter`                                         |
| `metrics.image.tag`                       | Exporter image tag                                  | `{TAG_NAME}`                                                      |
| `metrics.image.pullPolicy`                | Exporter image pull policy                          | `IfNotPresent`                                                    |
| `metrics.resources`                       | Exporter resource requests/limit                    | `nil`                                                             |
| `metrics.serviceMonitor.enabled`          | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`)                    | `false`                                                             |
| `metrics.serviceMonitor.namespace`        | Optional namespace which Prometheus is running in   | `nil`                                                             |
| `metrics.serviceMonitor.interval`         | How frequently to scrape metrics (use by default, falling back to Prometheus' default)  | `nil`                                                             |
| `metrics.serviceMonitor.selector`         | Default to kube-prometheus install (CoreOS recommended), but should be set according to Prometheus install                    | `{ prometheus: kube-prometheus }`                                                             |

The above parameters map to the env variables defined in [bitnami/mariadb](http://github.com/bitnami/bitnami-docker-mariadb). For more information please refer to the [bitnami/mariadb](http://github.com/bitnami/bitnami-docker-mariadb) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set rootUser.password=secretpassword,db.user=app_database \
    stable/mariadb
```
