**compile kubernetes:**

**依照**[**https://github.com/kubernetes/kubernetes/blob/release-1.2/build/README.md**](https://github.com/kubernetes/kubernetes/blob/release-1.2/build/README.md)

**到kubernetes/build 下 ./run.sh make**

**若遇到 cp: 無法 stat ‘build/build-image/Dockerfile’: 沒有此一檔案或目錄**

**進入kubernetes/build/common.sh檔案**

**更改kube::build::build\_image\(\) function裡面**

**將 cp build/build-image/Dockerfile .........**

**改成絕對路徑 ex： cp /home/william/kubernetes/build/build-image/Dockerfile .....**

**下面的另一個cp指令也改成絕對路徑 即可解決問題**

**binary會位於 /kubernetes/\_output/dockerized/bin/linux/amd64**

**將裡面的binary**

**kubectl → /kubernetes/cluster/ubuntu/binaries**

**kube-apiserver、kube-controller-manager、kube-scheduler**

**→ /kubernetes/cluster/ubuntu/binaries/master**

**kube-proxy、kubelet → /kubernetes/cluster/ubuntu/binaries/minion**

**然後重新deploy**

