## 網路設定 {#網路設定}

---

#### 圖形化介面 {#圖形化介面}

直接透過GUI設定。

#### 命令行介面 {#命令行介面}

##### 1. 修改網路介面設定檔 {#1-修改網路介面設定檔}

```
vim /etc/network/interfaces
```

* auto interface – 開機時啟動interface
* allow-hotplug interface – 偵測到新加入的interface時自動啟動他
* loopback – 連回自己
* inet static – 設定固定IP
* inet dhcp – 透過DHCP取得IP

```
auto lo  #lo為locate即127.0.0.1
iface lo inet loopback

#ethernet
allow-hotplug eth0
iface eth0 inet static
address xxx.xxx.xxx.xxx
netmask xxx.xxx.xxx.xxx
gateway xxx.xxx.xxx.xxx
dns-nameservers 8.8.8.8

#wifi
allow-hotplug wlan0
iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
iface default net dhcp
```

##### 2. 設定欲連線的WiFi AP {#2-設定欲連線的wifi-ap}

```
vim /etc/wpa_supplicant/wpa_supplicant.conf
```

格式為

```
network={
  ssid="xxx"
  psk="xxx"
}
```

可直接輸入指令

```
echo 'network={
  ssid="NMSL"
  psk="nmslinnthu"
}' | sudo tee -a /etc/wpa_supplicant/wpa_supplicant.conf
```

##### 3. 儲存變更 {#3-儲存變更}

`sudo /etc/init.d/networking restart`

> 參考1：[Good detailed explanation of /etc/network/interfaces syntax?](https://unix.stackexchange.com/questions/128439/good-detailed-explanation-of-etc-network-interfaces-syntax)

> 參考2：[有線 或 無線 的DHCP 設定或固定IP設定](https://sites.google.com/site/raspberypishare0918/home/di-yi-ci-qi-dong/1-6-you-xian-huo-wu-xian-dedhcp)

#### 問題 {#問題}

* `ping`不到 8.8.8.8 —&gt;DNS無法正常運作
  * 修改 /etc/resolv.conf 加上 nameserver 8.8.8.8
* `ifconfig -a`找不到介面卡
  * 重置介面卡`ifdown eth0`、`ifup eth0`



