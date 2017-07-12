# 安裝作業系統 {#安裝作業系統}

---

### 下載Image {#下載image}

* [Raspbian](https://www.raspberrypi.org/downloads/raspbian/)
  * Raspberry Pi官方推薦的Image
* [Hypriot Docker](http://blog.hypriot.com/downloads/)
  * 內建Docker的Image
* [kubernetes-on-arm](https://github.com/luxas/kubernetes-on-arm)
  * 將Kubernetes整合進ARM系統的project，有script可以幫助燒錄SD卡

### 燒錄SD卡 {#燒錄sd卡}

```
#列出Disk狀態
diskutil list

#unmount要燒錄的對象
diskutil unmountDisk /dev/disk4

#進行燒錄，bs=<處理速度> if=<輸入> of=<輸出>

#所以要備份的話只要將if和of倒過來就可以了
sudo dd bs=1m if=2016-05-27-raspbian-jessie.img of=/dev/rdisk4
```

> 參考 :[INSTALLING OPERATING SYSTEM IMAGES ON MAC OS](https://www.raspberrypi.org/documentation/installation/installing-images/mac.md)

### 空間調整 {#空間調整}

將SD卡插入Pi開機後輸入`df -h`指令會發現總空間只跟image一樣大，且使用率已接近100%，因此必須進行空間的調整，將SD卡剩餘的空間合併過來

* 透過內建選單\(較迅速\)

  ```
  sudo raspi-config
  #選擇第一項Expand Filesystem
  #大功告成！
  ```

* 透過指令\(較繁瑣\)

  ```
  sudo fdisk /dev/mmcblk0
  #1.輸入'p'取得目前分割狀態，然後**把第二塊分割區域的起始位置記錄下來**
  #2.輸入'd'來刪除分區，接著他會問你要刪哪一塊，這時候輸入'2'
  #3.輸入'd'以及'3'把第三區也刪除掉
  #4.輸入'n'來建立新的分區，接著輸入'p'和'2'表示建立一個primary的第二區
  #5.接著輸入分區的起始位置，也就是在第一步驟時記錄下來的那個數字
  #6.輸入enter，分區的結束位置為default值
  #7.輸入'w'，儲存剛剛所有的設定

  #重新開機
  sudo reboot

  #進行空間調整
  sudo resize2fs /dev/mmcblk0p2

  #再重新開機一次
  sudo reboot

  #大功告成！
  df -h
  ```

  > 參考：[How can I resize my / \(root\) partition?](https://raspberrypi.stackexchange.com/questions/499/how-can-i-resize-my-root-partition)

[            
](https://wakeuptsai.gitbooks.io/nmsl-fog-computing-platform/content/raspberry-pi.html)

