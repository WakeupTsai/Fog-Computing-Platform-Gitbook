# kubeadm {#kubeadm}

---

### 安裝 {#安裝}

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

### 操作 {#操作}

* ##### 啟動Master {#啟動master}

  ```
  kubeadm init

  #接著會出現以下訊息
  [kubeadm] WARNING: kubeadm is in alpha, please do not use it for production clusters.
  [preflight] Running pre-flight checks
  [init] Using Kubernetes version: v1.5.1
  [tokens] Generated token: "7914ed.1ea34eae5cab9e8c"
  [certificates] Generated Certificate Authority key and certificate.
  [certificates] Generated API Server key and certificate
  [certificates] Generated Service Account signing keys
  [certificates] Created keys and certificates in "/etc/kubernetes/pki"
  [kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/kubelet.conf"
  [kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/admin.conf"
  [apiclient] Created API client, waiting for the control plane to become ready
  [apiclient] All control plane components are healthy after 30.814512 seconds
  [apiclient] Waiting for at least one node to register and become ready
  [apiclient] First node is ready after 3.535811 seconds
  [apiclient] Creating a test deployment
  [apiclient] Test deployment succeeded
  [token-discovery] Created the kube-discovery deployment, waiting for it to become ready
  [token-discovery] kube-discovery is ready after 13.002653 seconds
  [addons] Created essential addon: kube-proxy
  [addons] Created essential addon: kube-dns

  Your Kubernetes master has initialized successfully!

  You should now deploy a pod network to the cluster.
  Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
      http://kubernetes.io/docs/admin/addons/

  You can now join any number of machines by running the following on each node:

  #這一行就是用來將node加入cluster的指令
  kubeadm join --token=[token] [master-IP]
  ```
* ##### 將node加入cluster {#將node加入cluster}

  ```
  kubeadn join --token=[token] [master-ip]

  #出現以下訊息就表示成功了
  [kubeadm] WARNING: kubeadm is in alpha, please do not use it for production clusters.
  [preflight] Running pre-flight checks
  [tokens] Validating provided token
  [discovery] Cluster info object received, verifying signature using given token
  [bootstrap] Detected server version: v1.5.1
  [bootstrap] Successfully established connection with endpoint "https://140.114.79.83:6443"
  [csr] Created API client to obtain unique certificate for this node, generating keys and certificate signing request
  [csr] Received signed certificate from the API server:
  Issuer: CN=kubernetes | Subject: CN=system:node:black-pearl | CA: false
  Not before: 2017-01-04 02:44:00 +0000 UTC Not After: 2018-01-04 02:44:00 +0000 UTC
  [csr] Generating kubelet configuration
  [kubeconfig] Wrote KubeConfig file to disk: "/etc/kubernetes/kubelet.conf"

  Node join complete:
  * Certificate signing request sent to master and response
    received.
  * Kubelet informed of new secure connection details.

  #可以到master執行kubectl get nodes檢查node是否有成功加入
  Run 'kubectl get nodes' on the master to see this machine join.
  ```
* ##### 重置kubeadm {#重置kubeadm}

  kubeadm init不可以重複執行，若啟動master失敗想要重啟，都必須先進行重置

  ```
  kubeadm reset
  ```

### 問題 {#問題}

* error: couldn't read version from server
  * 若曾經安裝過舊版k8s則有可能是設定檔重複，刪除 ~/.kube/config即可



