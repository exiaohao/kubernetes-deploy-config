## See also
- Create cluster by kubeadm
https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/
- Install Calico
https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/calico

## Before begin
Make sure `kubeadm` `kubectl` and `kubelet` has installed and `systemctl status kubelet` has `active (running)` status

#### kubelet config
/etc/systemd/system/kubelet.service.d/

## Create kubernetes cluster
1. Edit `kubeadm-init-config.yml`, run `sudo kubeadm init --config=kubeadm-init-config.yml` to Init your new cluster, it applies `advertiseAddr`, `etcd endpoints`, `networking`, etc.
2. Remember line `kubeadm join`
3. run `kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/rbac.yaml`
4. Edit `calico.yaml`, set `etcd` and other configs, run `kubeadm apply -f calico.yaml`

## Troubleshooting
#### x509 certificate error
Run `kubectl ...` receive:
```Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "kubernetes")```

Realted issue: https://github.com/kubernetes/kubernetes/issues/48378

Add `$KUBECONFIG` to `/etc/kubernetes/kubelet.conf`

### RBAC error
Run `kubectl apply -f rbac.yaml` and receive:
```Error from server (Forbidden): error when retrieving current configuration of:
&{0xc420097980 0xc4203d7dc0  calico-kube-controllers rbac.yaml 0xc420c188c0  false}
from server for: "rbac.yaml": clusterroles.rbac.authorization.k8s.io "calico-kube-controllers" is forbidden: User "system:node:hao-k8s-1" cannot get clusterroles.rbac.authorization.k8s.io at the cluster scope```

Related issue: https://github.com/kubernetes/kops/issues/3551

Kubernetes Doc - https://kubernetes.io/docs/reference/access-authn-authz/rbac/


