## 安裝K8s \(Master + Worker共同步驟\)

1.先拉下要用的docker images

```
sudo docker pull http://quay.io/coreos/flannel:v0.10.0-amd64
```

2.更新resource link

```
sudo apt-get update \
  && sudo apt-get install -y apt-transport-https \
  && curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" \
  | sudo tee -a /etc/apt/sources.list.d/kubernetes.list \
  && sudo apt-get update
```

3.安裝kubeadm, kubelet, kubectl, k8s-cni

```
sudo apt-get install -y kubeadm=1.10.5-00 kubelet=1.10.5-00 kubectl=1.10.5-00 kubernetes-cni=0.6.0-00
```

## Master Only

4.關閉swap

```
sudo swapoff -a
sudo rm -f /swapfile
sudo vi /etc/fstab
#sudo swapon --summary
#cat /proc/swaps
```

5.安裝及啟動k8s

```
IP_ADDR=$(ip addr show eno1 | grep -Po 'inet \K[\d.]+')
echo $IP_ADDR
sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --apiserver-advertise-address=${IP_ADDR} --kubernetes-version stable-1.11

#成功後顯示
Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
```

1. ```
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```
2. deploy network

```
kubectl apply -f [podnetwork].yaml
#查看有哪些network https://kubernetes.io/docs/concepts/cluster-administration/addons/
```



