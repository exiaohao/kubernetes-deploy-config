## Istio

Deploy
```bash
istioctl create -f istio-aio.yaml
```

Add TLS certificate & key
```bash
kubectl create -n istio-system secret tls istio-ingressgateway-ca-certs --key hao.meshlab.cn.key --cert hao.meshlab.cn.crt
```
