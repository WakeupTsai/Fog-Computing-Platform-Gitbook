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

## Worker Only

4至Master端下此指令

```
kubeadm token create --print-join-command
#得類似以下指令 複製並至worker端下
#kubeadm join --token abcdef.1234567890abcdef --discovery-token-unsafe-skip-ca-verification 1.2.3.4:6443
```

5至worker端 連接至master

    kubeadm join --token abcdef.1234567890abcdef --discovery-token-unsafe-skip-ca-verification 1.2.3.4:6443`



