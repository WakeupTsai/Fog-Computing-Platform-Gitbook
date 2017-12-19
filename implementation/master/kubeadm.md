## kubeadm

---

#### 安裝

主要參考[官方文件](http://kubernetes.io/docs/getting-started-guides/kubeadm/)和這篇[網誌](http://www.evanlin.com/til-kubeadm/)，建議於Ubuntu16.04環境進行安裝，之前在14.04測試有滿多問題的
```
#安裝相關packages, 這裡省略docker的安裝 
apt-get install -y kubelet kubeadm kubectl kubernetes-cni
apt-get update && apt-get upgrade

#使用Ubuntu或HypriotOS的話需再執行以下指令
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF

```

#### 操作
- 啟動Master

```
kubeadm init

#接著會出現以下訊息
... ...
Your Kubernetes master has initialized successfully!

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
    http://kubernetes.io/docs/admin/addons/
```
```
You can now join any number of machines by running the following on each node:

kubeadm join --token=[token] [master-IP] # <--注意

```

- 將node加入cluster

```
kubeadn join --token=[token] [master-ip]

#出現以下訊息就表示成功了
... ...
Node join complete:
* Certificate signing request sent to master and response
  received.
* Kubelet informed of new secure connection details.

#可以到master執行kubectl get nodes檢查node是否有成功加入
Run 'kubectl get nodes' on the master to see this machine join.
```

- 重置kubeadm

kubeadm init不可以重複執行，若啟動master失敗想要重啟，都必須先進行重置

```
kubeadm reset
```

#### 問題

- error: couldn't read version from server
  - 若曾經安裝過舊版k8s則有可能是設定檔重複，刪除 ~/.kube/config即可