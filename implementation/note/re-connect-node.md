1. 從master端刪除node
每次要連的時候都要先從master把那個node刪掉
```kubectl get node``` 可以看目前有哪些node
然後打```kubectl delete node [node name]```
像是nmsl1就打 ```kubectl delete node nmsl1```

2. 到node端重新連線(這步驟有時候會出問題 狀況有點多種 遇到再問我)
pc的話是這樣：
	```
	cd fog_computing/k8s
	sudo bash worker.sh
	```
rpi則是：
	```
	sudo kube-config enable-worker 192.168.0.99
	```

3. 到master端檢查
```kubectl get node```看有沒有成功連上
成功的話到deploy資料夾底下執行```label_node```
重新label新連上的node