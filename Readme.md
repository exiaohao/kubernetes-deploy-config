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
