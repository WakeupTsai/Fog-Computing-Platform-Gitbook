# Helm
---
### 安裝

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

### 啟動

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

