# Install Operator
## Add Elasticsearch Helm Repositories
```
helm repo add elastic https://helm.elastic.co
helm repo update
```

## Install operator and CRDs (Not Cluster-wide)
#### Due to us needing the CRDs at the time of template installation we MUST install these items manually.
```
helm install elastic-operator-crds elastic/eck-operator-crds
```
```
#### Install CRDs outside of operator so cluster remains even if operator is deleted
#### We specify a namespace here, but you can opt to install it clusterwide

helm install elastic-operator elastic/eck-operator -n <Namespace> \
    --set=installCRDs=false \
    --set=managedNamespaces='{<Namespace>}' \
    --set=createClusterScopedResources=false \
    --set=webhook.enabled=false \
    --set=config.validateStorageClass=false
```

## Uninstall Operator and CRDs
```
helm uninstall elastic-operator-crds -n <Namespace>
helm uninstall elastic-operator -n <Namespace>
```

## Install deployments (ES (3 master/ 3 data) Kibana (1 instance))
```
helm install elastic-cloud --namespace <Namespace> -f values.yaml .
```

## Register snapshot repository S3
#### Snapshots will be saved in the following format snapshot-YYYY.MM.DD if you need to restore in the future
```
PUT _snapshot/my_backup
{
  "type": "s3",
  "settings": {
    "bucket": "<Bucket Name>",
    "region": "<Region>",
    "base_path": "backups"
  }
}
```