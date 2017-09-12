# Fog Computing Platform Master {#raspberry-pi硬體規格}

---

### Kubernetes {#圖形化介面}

* 安裝與啟動

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
ALLOW_PRIVILEGED=true KUBERNETES_PROVIDER=ubuntu ./kube-up.sh
```

> 參考：[Manually Deploying Kubernetes on Ubuntu Nodes](https://kubernetes.io/docs/getting-started-guides/ubuntu/manual/)

### Helm

* 安裝

```
# compile原始碼
cd $GOPATH
mkdir -p src/k8s.io
cd src/k8s.io
git clone https://github.com/kubernetes/helm.git
cd helm
make bootstrap build

mv bin/helm /usr/local/bin/helm
mv bin/tiller /usr/local/bin/tiller
```

* 啟動

```
# 啟動helm
helm init 
# 啟動tiller
bin/tiller
export HELM_HOST=localhost:44134
# 檢查是否成功
helm version
```

> 參考：[Installing Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md#installing-helm)

### Kubernetes Dashboard

* 利用k8s與container啟動dashboard

```
wget https://rawgit.com/kubernetes/dashboard/master/src/deploy/kubernetes-dashboard.yaml

# 將port expose出來，否則只能從localhost連入
# 於第65行加入"hostPort: [port]"
# 例如以下設定可以透過[master-ip]:[8888]進入dashboard
# - containerPort: 9090
#   hostPort: 8888
#   protocol: TCP
vim kubernetes-dashboard.yaml

# 佈建並啟動，完成！
kubectl create -f kubernetes-dashboard.yaml
```

* 手動安裝在local端

```
git clone https://github.com/kubernetes/dashboard.git
cd dashboard

# 安裝node.js
sudo apt-get update
sudo apt-get install build-essential libssl-dev
curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh
source ~/.profile
nvm install v6.11.3  # 版本自選
node -v

# 安裝go-lang，版本自選
wget https://storage.googleapis.com/golang/go1.9.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.9.linux-amd64.tar.gz
export PATH=$PATH:/usr/local/go/bin
echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
go version

# 安裝dependencies
npm install

# 安裝gulp
sudo npm install --global gulp-cli
sudo npm install --global gulp
gulp -v

# 啟動dashboard，port預設為9090
gulp serve
```

> 參考1：[Getting Started](https://github.com/kubernetes/dashboard/blob/master/docs/devel/getting-started.md)  
> 參考2：[Installing Requirements for the Kubernetes Dashboard](https://github.com/kubernetes/dashboard/blob/master/docs/devel/requirements-installation.md)  
> 參考3：[在 Ubuntu 14.04 上安裝 node.js](https://tw-hkt.gitbooks.io/blog/content/zai_ubuntu_14__04_shang_an_zhuang_node__js.html)

### MQTT-Panel

* 安裝與啟動

```
git clone https://github.com/WakeupTsai/FogComputingPlatform-MQTT-Panel.git
cd FogComputingPlatform-MQTT-Panel

# 安裝dependencies
npm install

# 設定環境變數
export MQTTPANELPORT=[port]  #若沒設定預設為5000
export MQTTBROKER=mqtt:[broker ip] #若沒設定預設為mqtt:m2m.eclipse.org

# 啟動mqtt-panel,完成後即可到localhost:[port]查看
npm start

# 可隨便publish一則訊息測試網頁是否正常
mosquitto_pub -h [broker ip] -t "lab/test" -m "test"
```



