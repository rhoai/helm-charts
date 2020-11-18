# Redis

## TL;DR;

```console
$ helm install rhoai/redis
```

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0-beta3+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `redis`:

```console
$ helm install --name redis rhoai/redis
```

## Uninstalling the Chart

To uninstall/delete the `redis` deployment:

```console
$ helm delete redis
```

## Parameters

See https://github.com/bitnami/charts/tree/master/bitnami/redis#parameters
