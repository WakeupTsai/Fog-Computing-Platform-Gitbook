# 安裝 {#raspberry-pi硬體規格}

---

### Docker CE v.s. Docker EE {#圖形化介面}

Docker在 1.13.1版之後將版本劃分為CE \(Community Edition\)和EE \(Enterprise Edition\)兩個分支，兩者的主要差別在於EE版提供了相對穩定且安全的環境，並支援許多商業級別的外掛程式，而CE版則為免費的開源專案，更新較為快速很適合開發者使用。

> 參考 :[Docker 17.03系列教程（一）Docker EE/Docker CE简介与版本规划](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)

### Docker CE

* 安裝

```
# 設定apt-get時的repository
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# 開始安裝docker-ce
sudo apt-get update
apt-cache madison docker-ce
sudo apt-get install docker-ce=<VERSION>

# 完成
sudo docker run hello-world
```

* 移除

```
sudo apt-get -y purge docker-ce
sudo apt-get -y autoremove

# 移除所有containers,images,volumes
sudo rm -rf /var/lib/docker
```

> 參考：[Get Docker CE for Ubuntu](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/)

### 舊版Docker

* 安裝

```
# 設定apt-get時的repository
sudo apt-get update
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-trusty main'
sudo apt-get update

# 開始安裝docker-engine
apt-cache policy docker-engine
sudo  apt-get install -y docker-engine=<VERSION>

# 完成
sudo docker run hello-world
```

* 移除

```
sudo apt-get -y purge docker-engine
sudo apt-get -y autoremove

# 移除所有containers,images,volumes
sudo rm -rf /var/lib/docker
```

### 問題

* [Using docker requires sudo ](https://github.com/docker/docker-snap/issues/1)
  ```
  sudo addgroup --system docker
  sudo adduser $USER docker
  newgrp docker
  ```
* [Docker can't connect to docker daemon](https://stackoverflow.com/questions/21871479/docker-cant-connect-to-docker-daemon)

  * `sudo usermod -aG docker $(whoami)`

* docker: Error response from daemon: client is newer than server \(client API version: xxx, server API version: xxx\).
  * `sudo rm -rf /var/lib/docker`



