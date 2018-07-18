### Disable all plugins except istio
```bash
helm template install/kubernetes/helm/istio --name istio --namespace istio-system --set sidecarInjectorWebhook.enabled=false --set galley.enabled=false --set mixer.enabled=false --set security.enabled=false --set pilot.enabled=false > ~/istio-cutted.yaml
```

### Deploy
```
# kubectl apply -f ./istio-cutted.yaml
configmap/prometheus created
configmap/istio created
configmap/istio-sidecar-injector created
serviceaccount/istio-egressgateway-service-account created
serviceaccount/istio-ingress-service-account created
serviceaccount/istio-ingressgateway-service-account created
serviceaccount/prometheus created
clusterrole.rbac.authorization.k8s.io/istio-ingress-istio-system configured
clusterrole.rbac.authorization.k8s.io/prometheus-istio-system configured
clusterrolebinding.rbac.authorization.k8s.io/prometheus-istio-system configured
clusterrolebinding.rbac.authorization.k8s.io/istio-ingress-istio-system configured
service/istio-egressgateway created
service/istio-ingress created
service/istio-ingressgateway created
service/prometheus created
deployment.extensions/istio-egressgateway created
deployment.extensions/istio-ingress created
deployment.extensions/istio-ingressgateway created
deployment.extensions/prometheus created
horizontalpodautoscaler.autoscaling/istio-egressgateway created
horizontalpodautoscaler.autoscaling/istio-ingress created
horizontalpodautoscaler.autoscaling/istio-ingressgateway created
```
