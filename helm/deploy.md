### Disable all plugins except istio
```bash
helm template install/kubernetes/helm/istio --name istio --namespace istio-system --set sidecarInjectorWebhook.enabled=false --set galley.enabled=false --set mixer.enabled=false --set security.enabled=false --set pilot.enabled=false > ~/istio-cutted.yaml
```

Only istio
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

Istio + Pilot
```
configmap/prometheus unchanged
configmap/istio unchanged
configmap/istio-sidecar-injector unchanged
serviceaccount/istio-egressgateway-service-account unchanged
serviceaccount/istio-ingress-service-account unchanged
serviceaccount/istio-ingressgateway-service-account unchanged
serviceaccount/istio-pilot-service-account created
serviceaccount/prometheus unchanged
customresourcedefinition.apiextensions.k8s.io/destinationpolicies.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/egressrules.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/routerules.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/virtualservices.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/destinationrules.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/serviceentries.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/gateways.networking.istio.io created
customresourcedefinition.apiextensions.k8s.io/policies.authentication.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/httpapispecs.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecbindings.config.istio.io created
customresourcedefinition.apiextensions.k8s.io/quotaspecs.config.istio.io created
clusterrole.rbac.authorization.k8s.io/istio-ingress-istio-system configured
clusterrole.rbac.authorization.k8s.io/istio-pilot-istio-system created
clusterrole.rbac.authorization.k8s.io/prometheus-istio-system configured
clusterrolebinding.rbac.authorization.k8s.io/prometheus-istio-system configured
clusterrolebinding.rbac.authorization.k8s.io/istio-ingress-istio-system configured
clusterrolebinding.rbac.authorization.k8s.io/istio-pilot-istio-system created
service/istio-egressgateway unchanged
service/istio-ingress unchanged
service/istio-ingressgateway unchanged
service/istio-pilot created
service/prometheus unchanged
deployment.extensions/istio-egressgateway configured
deployment.extensions/istio-ingress configured
deployment.extensions/istio-ingressgateway configured
deployment.extensions/istio-pilot created
deployment.extensions/prometheus unchanged
horizontalpodautoscaler.autoscaling/istio-egressgateway unchanged
horizontalpodautoscaler.autoscaling/istio-ingress unchanged
horizontalpodautoscaler.autoscaling/istio-ingressgateway unchanged
```
