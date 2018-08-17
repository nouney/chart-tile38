# Tile38

This is a helm chart to install [Tile38](http://tile38.com) on a Kubernetes cluster.

## TL;DR;

```bash
$ git clone https://github.com/nouney/chart-tile38
$ helm install chart-tile38
```

## Prerequisites

- Kubernetes 1.9+
- PV provisioner support in the underlying infrastructure (Only when persisting data)

## Configuration

The following table lists the configurable parameters of the PostgreSQL chart and their default values.

| Parameter                  | Description                                     | Default                                                    |
| -----------------------    | ---------------------------------------------   | ---------------------------------------------------------- |
| `image`                    | `tile38` image repository                       | `tile38/tile38`                                            |
| `imageTag`                 | `postgres` image tag                            | `1.12.13`                                                  |
| `imagePullPolicy`          | Image pull policy                               | `IfNotPresent`                                             |
| `service.port`             | TCP port                                        | `9851`                                                     |
| `service.type`             | k8s service type exposing ports, e.g. `NodePort`| `ClusterIP`                                                |
| `leader.persistentVolume.enabled`      | Create a volume to store Tile38 data            | true
| `leader.persistentVolume.existingClaim`| Provide an existing PersistentVolumeClaim       | `nil`                                          |
| `leader.persistentVolume.storageClass` | Storage class of backing PVC                    | `nil` (uses alpha storage class annotation)    |
| `leader.persistentVolume.accessMode`   | Use volume as ReadOnly or ReadWrite             | `ReadWriteOnce`                                |
| `leader.persistentVolume.annotations`  | Persistent Volume annotations                   | `{}`                                           |
| `leader.persistentVolume.size`         | Size of data volume                             | `2Gi`                                          |
| `leader.persistentVolume.subPath`      | Subdirectory of the volume to mount at          | ``                                             |
| `leader.persistentVolume.mountPath`    | Mount path of data volume                       | `/data`                                        |
| `leader.resources`                | CPU/Memory resource requests/limits             | {}                                                         |
| `leader.nodeSelector`             | Node labels for pod assignment                  | {}                                                         |
| `leader.affinity`                 | Affinity settings for pod assignment            | {}                                                         |
| `leader.tolerations`              | Toleration labels for pod assignment            | []                                                         |
| `follower.persistentVolume.enabled`      | Create a volume to store Tile38 data            | true
| `follower.persistentVolume.existingClaim`| Provide an existing PersistentVolumeClaim       | `nil`                                          |
| `follower.persistentVolume.storageClass` | Storage class of backing PVC                    | `nil` (uses alpha storage class annotation)    |
| `follower.persistentVolume.accessMode`   | Use volume as ReadOnly or ReadWrite             | `ReadWriteOnce`                                |
| `follower.persistentVolume.annotations`  | Persistent Volume annotations                   | `{}`                                           |
| `follower.persistentVolume.size`         | Size of data volume                             | `2Gi`                                          |
| `follower.persistentVolume.subPath`      | Subdirectory of the volume to mount at          | ``                                             |
| `follower.persistentVolume.mountPath`    | Mount path of data volume                       | `/data`                                        |
| `follower.resources`                | CPU/Memory resource requests/limits             | {}                                                         |
| `follower.nodeSelector`             | Node labels for pod assignment                  | {}                                                         |
| `follower.affinity`                 | Affinity settings for pod assignment            | {}                                                         |
| `follower.tolerations`              | Toleration labels for pod assignment            | []                                                         |


### Existing PersistentVolumeClaims

1. Create the PersistentVolume
1. Create the PersistentVolumeClaim
1. Install the chart
```bash
$ helm install --set leader.persistentVolume.existingClaim=PVC_NAME chart-tile38
```