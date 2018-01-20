## MQTT-Panel

---

#### MQTT 安裝

```
# 安裝mqtt-broker
wget https://mosquitto.org/files/source/mosquitto-1.4.10.tar.gz
tar zxvf mosquitto-1.4.10.tar.gz
cd mosquitto-1.4.10/
sudo make prefix=/usr install
```

```
sudo vim /etc/init.d/rc.local
```

＃至檔案中最末加上一行 使一開機就將mosquitto在root 背景執行

```
mosquito -d
```

#### 安裝與啟動

```
git clone https://github.com/WakeupTsai/FogComputingPlatform-MQTT-Panel.git
cd FogComputingPlatform-MQTT-Panel

# 安裝dependencies
npm install

# 設定環境變數
export MQTTPANELPORT=[port]  #若沒設定預設為5000
export MQTTBROKER=mqtt:[broker ip] #若沒設定預設為mqtt:m2m.eclipse.org

# 啟動mqtt-panel,完成後即可到localhost:[port]查看
npm start

# 可隨便publish一則訊息測試網頁是否正常
mosquitto_pub -h [broker ip] -t "lab/test" -m "test"
```



