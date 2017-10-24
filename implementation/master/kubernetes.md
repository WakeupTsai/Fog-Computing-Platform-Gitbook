# Kubernetes {#raspberry-pi硬體規格}

---

### 安裝與啟動

```
# 使用1.5版本的Kubernetes
git clone -b release-1.5 --depth 1 https://github.com/kubernetes/kubernetes.git

# 修改code，將第45行的"verify-kube-binaries"註解掉
cd kubernetes/cluster
vim kube-up.sh

# 設定環境變數,nodes="[master-username]@[master-ip]"用來設定master是誰
export KUBE_VERSION=1.5.0 
export FLANNEL_VERSION=0.5.0 
export ETCD_VERSION=3.0.0 
export nodes="[master-username]@[master-ip]" 
export role="ai" 
export NUM_NODES=${NUM_NODES:-1} 
export SERVICE_CLUSTER_IP_RANGE=192.168.3.0/24 
export FLANNEL_NET=172.16.0.0/16

# 啟動kubernetes master
ALLOW_PRIVILEGED=true KUBERNETES_PROVIDER=ubuntu ./kube-up.sh

# 關閉kubernetes master
ALLOW_PRIVILEGED=true KUBERNETES_PROVIDER=ubuntu ./kube-down.sh
```

> 參考：[Manually Deploying Kubernetes on Ubuntu Nodes](https://kubernetes.io/docs/getting-started-guides/ubuntu/manual/)

### 問題
    - Could not find or add an SSH identity. Please start ssh-agent, add your identity, and retry.
    ```
	eval "$(ssh-agent)"
	ssh-keygen
	ssh-add /home/nmsl-master/.ssh/id_rsa
    ```
    > 參考：https://github.com/kubernetes/kubernetes/issues/11916


