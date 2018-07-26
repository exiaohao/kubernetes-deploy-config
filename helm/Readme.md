### Install

#### Create template with HELM
```
helm template install/kubernetes/helm/istio --name istio --namespace istio-system --set sidecarInjectorWebhook.enabled=false --set galley.enabled=false > ~/istio-with-mixer.yaml
```

#### Install istio (with customized components)
```
kubectl apply -f CUSTOMIZED_FILE.yaml
```

#### Functional verification
##### TLS support
- [x] TLSv1
- [x] TLSv1.1
- [x] TLSv1.2

#### Multiple certificates in single ingress
##### Default 
Only support *ONE* certificate


#### Troubleshooting

##### Mixer not available
Result
```bash
[libprotobuf ERROR src/istio/mixerclient/report_batch.cc:83] Mixer Report failed with: UNAVAILABLE:Cluster not available
```
Caused by CheckServer & ReportServer aren't applied with NON-Mixer environment, there's no endpoints to collect data

```
# To disable the mixer completely (including metrics), comment out
# the following lines
mixerCheckServer: istio-policy.istio-system.svc.cluster.local:15004
mixerReportServer: istio-telemetry.istio-system.svc.cluster.local:15004
```


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
 
