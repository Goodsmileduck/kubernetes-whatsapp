# WhatsApp Business API

## Introduction

This chart bootstraps a single node or multiconnect WhatsApp Business API deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

### Some features available in chart comparing to official manifests:

- Ingress resource
- Provides preconfigured database deployment (mysql/postgres)
- Database upgrades runs on any helm release upgrade (post-upgrade hook)
- Might be configured to use shared storages (EFS/NFS/Ceph) for media files
- Cronjob which delete media files by schedule from volume
- Changes admin password after installation (post-install hook)
- Web deployment has liveness Probe using WA_API_KEY

## Prerequisites

- Kubernetes 1.9+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

Add repo first:

```bash
helm repo add whatsapp https://goodsmileduck.github.io/kubernetes-whatsapp/
```

To install the chart with the release name `whatsapp`:

```bash
$ helm install whatsapp whatsapp/kubernetes-whatsapp
```

The command deploys WhatsApp Business API on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

By default helm deploys multiconnect node deployment.

To deploy single node deployment use file [values-single.yaml](templates/values-single.yaml)
> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `whatsapp` deployment:

```bash
$ helm delete --purge whatsapp
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the WhatsApp chart and their default values.

| Parameter       | Description                               | Default    |
| --------------- |-------------------------------------------|------------|
| `multiconnect`  | Multiconnect mode. Could be MYSQL or PGSQL| `False`    |
| `db.engine`     | Database engine                           | `MYSQL`    |
| `db.host`       | Hostname to access database               | `[]`       |

## TODO

* Update docs for configuration
* Add Healthcheck for core/web containers
* Update volume configuration
* Add affinitiy support
* Add tests
