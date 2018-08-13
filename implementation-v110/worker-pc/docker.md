## 安裝Docker-CE \(v17.02\)

```
#允許通過HTTPS使用儲存庫
sudo apt-get install \
     apt-transport-https \
     ca-certificates \
     curl \
     software-properties-common
#導入官方GPG密鑰
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
#選擇穩定版本
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
# 開始安裝docker-ce
sudo apt-get update
apt-cache madison docker-ce  #查看可安裝的版本
sudo apt-get install docker-ce=<VERSION>  #選擇要安裝的版本
e.g., sudo apt-get install docker-ce=17.02.0~ce-0~ubuntu

# 完成
sudo docker run hello-world
```



