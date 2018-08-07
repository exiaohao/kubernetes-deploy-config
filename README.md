## Namespace
Concepts 
https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

#### Command
```bash
kubectl create namespace [NAMESPACE-NAME]
```
#### Format
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: test-space
```

## Login private registry
```bash
kubectl create secret docker-registry [SECRET-NAME] --docker-server=[REGISTRY-SERVER] --docker-username=[DOCKER-USERNAME] --docker-password=[DOCKER-PASSWORD] --docker-email=[DOCKER-EMAIL] -n [NAMESPACE]
```

## Get admin token
```bash
kubectl -n kube-system describe secret `kubectl -n kube-system get secret|grep admin-token|cut -d " " -f1` | grep "token:" | tr -s " " | cut -d " " -f2
```
