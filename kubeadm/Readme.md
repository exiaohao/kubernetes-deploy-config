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
1. Edit `kubeadm-init-config.yml`, run `kubeadm init --config=kubeadm-init-config.yml` to Init your new cluster, it applies `advertiseAddr`, `etcd endpoints`, `networking`, etc.
2. Remember line `kubeadm join`
3. run `kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/rbac.yaml`
4. Edit `calico.yaml`, set `etcd` and other configs, run `kubeadm apply -f calico.yaml`

## Troubleshooting
Run `kubectl ...` receive:
```Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "kubernetes")```

Realted issue: https://github.com/kubernetes/kubernetes/issues/48378

Add `$KUBECONFIG` to `/etc/kubernetes/kubelet.conf`
