# Install Operator
## Add Elasticsearch Helm Repositories
```
helm repo add elastic https://helm.elastic.co
helm repo update
```

## Install operator and CRDs (Not Cluster-wide)
#### Due to us needing the CRDs at the time of template installation we MUST install these items manually.
```
helm install elastic-operator elastic/eck-operator -n <Namespace> \
    --set=installCRDs=true \
    --set=managedNamespaces='{<Namespace>}' \
    --set=createClusterScopedResources=false \
    --set=webhook.enabled=false \
    --set=config.validateStorageClass=false
```

# Uninstall Operator
```
helm uninstall elastic-operator-crds -n <Namespace>
helm uninstall elastic-operator -n <Namespace>
```

## Install deployments (ES (3 master/ 3 data) Kibana (1 instance))
```
helm install elastic-cloud --namespace <Namespace> -f values.yaml .
```

## Register snapshot repository S3
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