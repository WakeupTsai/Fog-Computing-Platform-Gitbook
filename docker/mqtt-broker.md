# mqtt-broker

---
### 安裝
```
wget http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key
sudo apt-key add mosquitto-repo.gpg.key
cd /etc/apt/sources.list.d/
sudo wget http://repo.mosquitto.org/debian/mosquitto-wheezy.list

sudo apt-get update
sudo apt-get install mosquitto
```

### 帳號密碼設定
```
mosquitto_passwd -c /etc/mosquitto/passwd [user account]
# 接下來會要求輸入密碼

# 修改mosquitto設定檔
vim /etc/mosquitto/mosquitto.conf
# 加入以下兩行
password_file /etc/mosquitto/passwd # 設定帳號密碼檔案
allow_anonymous false # 禁止匿名登入

# 重啟service
service mosquitto restart

# 測試
mosquitto_sub -h [broker] -t test -u [user] -P [passwd]
mosquitto_pub -h [broker] -t test -u [user] -P [passwd] -m "Hello, world!"
```

### SSL/TlS
```
mkdir myCA
chmod 700 myCA
cd myCA

# 創建CA並生成server端證書
wget https://github.com/owntracks/tools/raw/master/TLS/generate-CA.sh
bash generate-CA.sh

# 將金鑰複製到 Mosquitto 的目錄之中：
sudo cp ca.crt /etc/mosquitto/certs/
sudo cp xxxxx.crt xxxxx.key /etc/mosquitto/certs/

# 修改mosquitto設定檔
vim /etc/mosquitto/mosquitto.conf
# 加入以下三行
cafile /etc/mosquitto/certs/ca.crt
certfile /etc/mosquitto/certs/xxxxx.crt
keyfile /etc/mosquitto/certs/xxxxx.key

# 重啟service
service mosquitto restart

# 測試
mosquitto_pub -h [broker] -t test -m 'test' -u [user] -P [passwd] --cafile ca.crt
mosquitto_sub -h [broker] -t test -u [user] -P [passwd] --cafile --cafile ca.crt
```


> 參考1：[樹莓派安裝 Mosquitto 輕量級 MQTT Broker 教學，連接各種物聯網設備](https://blog.gtwang.org/iot/raspberry-pi/raspberry-pi-mosquitto-mqtt-broker-iot-integration/2/)
> 參考2：[Setting up Authentication in Mosquitto MQTT Broker](https://medium.com/@eranda/setting-up-authentication-on-mosquitto-mqtt-broker-de5df2e29afc)
> 參考3：[在MQTT中使用SSL/TLS提高安全性](http://www.itdadao.com/articles/c15a749417p0.html)
> 參考4：[Mosquitto MQTT 安裝](https://ming-yi.github.io/2016/08/17/Mosquitto%20MQTT%20安裝/)