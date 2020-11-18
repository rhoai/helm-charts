# Postgres

## TL;DR;

```console
$ helm install rhoai/postgresql
```

## Prerequisites

- Kubernetes 1.12+
- Helm 3.0-beta3+
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `postgresql`:

```console
$ helm install --name postgresql rhoai/postgresql
```

## Uninstalling the Chart

To uninstall/delete the `postgresql` deployment:

```console
$ helm delete postgresql
```

## Parameters

See https://github.com/bitnami/charts/tree/master/bitnami/postgresql#parameters
