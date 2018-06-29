## See also
- Create cluster by kubeadm
https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/
- Install Calico
https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/calico

## Create kubernetes cluster
1. Edit `kubeadm-init-config.yml`, run `kubeadm apply -f ~`. Apply `advertiseAddr`, `etcd endpoints`, `networking`, etc.
2. run `kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/rbac.yaml`
3. Edit `calico.yaml`, set `etcd` and other configs, run `kubeadm apply -f calico.yaml`
