## Istio

Enable grafana
```bash
kubectl apply -f install/kubernetes/addons/grafana.yaml
```

Deploy
```bash
istioctl create -f istio-aio.yaml
```

#### Add TLS certificate & key
Add key & certificate to secret
```bash
kubectl create -n istio-system secret tls istio-ingressgateway-ca-certs --key hao.meshlab.cn.key --cert hao.meshlab.cn.crt
```
> The secret MUST be called `istio-ingressgateway-certs` in the `istio-system` namespace, or it will not be mounted and available to the Istio gateway.
> Thus generally only support ONE certificate

Define a Gateway with a server section for https/443.
```yaml
spec:
  selector:
    istio: ingressgateway
  servers:
  - port:
      number: 443
      name: https
      protocol: HTTPS
    hosts:
    - "hao.meshlab.cn"
    tls:
      mode: SIMPLE #enables HTTPS on this port
      serverCertificate: /etc/istio/ingressgateway-certs/tls.crt
      privateKey: /etc/istio/ingressgateway-certs/tls.key
```
> The location of the certificate and key MUST be `/etc/istio/ingressgateway-certs`, or the gateway will fail to load them.

To check the certificate and key was successfully loaded by istio gateway, use
```bash
kubectl exec -it -n istio-system $(kubectl -n istio-system get pods -l istio=ingressgateway -o jsonpath='{.items[0].metadata.name}') -- ls -al /etc/istio/ingressgateway-certs
```
will show you tls.key & tls.crt was mounted into ingressgateway

## Functional verification
#### TLS support
- [x] TLSv1
- [x] TLSv1.1
- [x] TLSv1.2

#### Multiple certificates in single ingress
##### Default 
Only support *ONE* certificate

#### More certificates
1. Listen to same port 443(any other you want)
2. Add corresponding domain name and certificate

example:
```yaml
spec:
  selector:
    istio: ingressgateway # use Istio default gateway implementation
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "hao.meshlab.cn"
    - "test-service-a.deploy.com"
    - "test-service-b.deploy.com"
  - port:
      number: 443
      name: https
      protocol: HTTPS
    hosts:
    - "hao.meshlab.cn"
    - "test-service-a.deploy.com"
    - "test-service-b.deploy.com"
    tls:
      mode: SIMPLE #enables HTTPS on this port
      serverCertificate: /etc/istio/ingressgateway-certs/tls.crt
      privateKey: /etc/istio/ingressgateway-certs/tls.key
  - port:
      number: 443
      name: https
      protocol: HTTPS
    hosts:
    - "static.cloudeliver.cn"
    tls:
      mode: SIMPLE
      serverCertificate: /root/tls-certs/static.cloudeliver.cn.crt
      privateKey: /root/tls-certs/static.cloudeliver.cn.key
```

view full yaml: istio-aio-mulitple-certs.yaml
