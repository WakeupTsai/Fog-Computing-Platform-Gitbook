## Heapster
---
Heapster是容器集群監控和性能分析工具，支持Kubernetes和CoreOS。

Kubernetes有個出名的監控代理--- cAdvisor。在每個kubernetes Node上都會運行cAdvisor，它會收集本機以及容器的監控數據（cpu，內存，文件系統，網絡，正常運行時間）。

在較新的版本中，K8S已經將cAdvisor功能集成到kubelet組件中。每個節點節點可以直接進行網絡訪問。

    > cAdvisor web界面訪問：http：// <Node-IP>：4194

Heapster是一個收集者，將每個節點上的cAdvisor的數據進行匯總，然後導到第三方工具（如InfluxDB和K8S Dashboard)。
![](/assets/b0d99354cc806ed488244bfec7cbc800.png)

> 參考：[Kubernetes监控之Heapster介绍](http://dockone.io/article/1881)

* 執行於Container當中

```
git clone https://github.com/kubernetes/heapster
cd heapster

kubectl create -f deploy/kube-config/influxdb/heapster.yaml
# kubectl create -f deploy/kube-config/rbac/heapster-rbac.yaml
```