## Kiali

**Requirements**
- Prometheus
- Grafana
- Serviceaccount with permissions

**Enable kiali**

Helm enable related configs
```bash
helm template --set kiali.enabled=true
```

Create kiali username & password
```bash
$ KIALI_USERNAME=$(read -p 'Kiali Username: ' uval && echo -n $uval | base64)
$ KIALI_PASSPHRASE=$(read -sp 'Kiali Passphrase: ' pval && echo -n $pval | base64)
```

Create secret with following username & password
```yaml
NAMESPACE=istio-system
kubectl create namespace $NAMESPACE
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: kiali
  namespace: $NAMESPACE
  labels:
    app: kiali
type: Opaque
data:
  username: $KIALI_USERNAME
  passphrase: $KIALI_PASSPHRASE
EOF
```

**Permissions**

Errors like
`Cannot load the graph: jobs.batch is forbidden: User "system:serviceaccount:istio-system:kiali-service-account" cannot list jobs.batch in the namespace "default"`

ClusterRole add `jobs.batch`
```yaml
- apiGroups:
  - batch
  resources:
  - cronjobs
  verbs:
  - get
  - list
  - watch
  - delete
  - deletecollection
```

Errors like
`Cannot load the graph: replicationcontrollers is forbidden: User "system:serviceaccount:istio-system:kiali-service-account" cannot list replicationcontrollers in the namespace "default"`
Add permissions to `apps` node
