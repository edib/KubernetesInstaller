# KubernetesInstaller
Simple and Working Kubernetes Installer
## For all

*** On Ubuntu 16.04
```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```
```
apt-get update && apt-get install docker-ce
```

### Add key for new repository:
```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

### Add repository:
```
sudo echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >> /etc/apt/sources.list.d/kubernetes.list
```

### Install Kubernetes:
```
apt-get update && apt-get install -y kubelet kubeadm kubectl
```

### Run only on master
```
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubeadm init --pod-network-cidr=<a_16bit_subnet>/16 --apiserver-advertise-address=<master_ip>
```

#### Return Message should be like this
---
Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:
kubeadm join --token <some_tokens> <master_ip>:6443 --discovery-token-ca-cert-hash sha256:<some_hash>

### Run only on nodes (minions)
```
kubeadm join --token <some_tokens> <master_ip>:6443 --discovery-token-ca-cert-hash sha256:<some_hash>
```

*** Reference: https://www.mirantis.com/blog/how-install-kubernetes-kubeadm/
