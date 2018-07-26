## Istio

Deploy
```bash
istioctl create -f istio-aio.yaml
```

Add TLS certificate & key
```bash
kubectl create -n istio-system secret tls istio-ingressgateway-ca-certs --key hao.meshlab.cn.key --cert hao.meshlab.cn.crt
```

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
