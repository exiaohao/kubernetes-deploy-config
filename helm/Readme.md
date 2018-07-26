### Install

#### Create template with HELM
```
helm template install/kubernetes/helm/istio --name istio --namespace istio-system --set sidecarInjectorWebhook.enabled=false --set galley.enabled=false > ~/istio-with-mixer.yaml
```

#### Install istio (with customized components)
```
kubectl apply -f CUSTOMIZED_FILE.yaml
```

#### Troubleshooting

##### configmaps is forbidden
```bash
helm list
```
Result:
`Error: configmaps is forbidden: User "system:serviceaccount:kube-system:default" cannot list configmaps in the namespace "kube-system"`

```bash
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'      
helm init --service-account tiller --upgrade
```
 
