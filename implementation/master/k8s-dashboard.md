## Kubernetes Dashboard
---
#### 利用k8s與container啟動dashboard

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
#### 手動安裝在local端
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
> 參考1：[Getting Started](https://github.com/kubernetes/dashboard/wiki/Getting-started)
> 參考2：[在 Ubuntu 14.04 上安裝 node.js](https://tw-hkt.gitbooks.io/blog/content/zai_ubuntu_14__04_shang_an_zhuang_node__js.html)

#### 問題
* 如果啟動後出現以下Warning表示Heapster沒有執行
```Metric client health check failed: the server could not find the requested resource (get services heapster). Retrying in 30 seconds.```



