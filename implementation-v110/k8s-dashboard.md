[https://github.com/kubernetes/dashboard/wiki/Getting-started](https://github.com/kubernetes/dashboard/wiki/Getting-started)

# Installation for Dashboard

### 1. Git Clone Dashboard

```
$ git clone https://github.com/kubernetes/dashboard.git
$ cd dashboard
```

### 2. Golang 1.8+

```
# Installation
$ wget https://dl.google.com/go/go1.11.2.linux-amd64.tar.gz
$ sudo tar -C /usr/local -xzf go1.11.2.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
$ echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.profile
$ go version
```

```
# Test
$ mkdir hello
$ cd hello
$ vim hello.go
```

```
#######inside the hello.go ##########
package main

import "fmt"

func main() {
    fmt.Printf("hello, world\n")
}
######################################
```

```
$ go build
$ ./hello
hello, world
#成功！！
```

### 3. Node.js 8+ and npm 5+

```
sudo apt-get update
sudo apt-get install build-essential libssl-dev
curl https://raw.githubusercontent.com/creationix/nvm/v0.16.1/install.sh | sh
source ~/.profile
nvm install v8.9.1  # 版本自選
node -v

# 安裝dependencies
npm install
```

### 4. Java7+

```
$ sudo apt-get install openjdk-8-jre
```

### 5. Gulp.js 3.9+

```
$ npm install --global gulp-cli
$ npm install --global gulp
# Check
$ gulp --version
```

### 6. Heapster

```
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/grafana.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/heapster.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/influxdb/influxdb.yaml
kubectl create -f https://raw.githubusercontent.com/kubernetes/heapster/master/deploy/kube-config/rbac/heapster-rbac.yaml
```

### Run Dashboard

```
# 讓api server 有對外的port可以連到
kubectl proxy --port=8080
# 啟動dashboard，port預設為9090
gulp serve
```



