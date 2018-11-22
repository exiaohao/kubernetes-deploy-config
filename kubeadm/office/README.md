# Office Cluster

Init cluster
```bash
apt-get update && apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
apt-key fingerprint 0EBFCD88

add-apt-repository    "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
	$(lsb_release -cs) \
	stable"

cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF

apt-get update

apt-get install docker-ce=17.03.3~ce-0~ubuntu-xenial
apt install -y kubelet=1.11.0-00 kubectl=1.11.0-00 kubeadm=1.11.0-00

systemctl daemon-reload
systemctl restart docker
systemctl restart kubelet
```

Addresses
- etcd: http://100.100.62.193:2379
- calico ipv4 pool: 10.100.0.0/16
- cluster IPs: 100.100.62.193-196

Create Kubernetes Cluster
```bash
kubeadm init --config=kubeadm-init-config.yaml
kubectl apply -f https://docs.projectcalico.org/v3.1/getting-started/kubernetes/installation/rbac.yaml
kubectl apply -f calico.yaml
```
