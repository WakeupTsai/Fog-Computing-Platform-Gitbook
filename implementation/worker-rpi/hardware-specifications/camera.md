#### Camera

* 啟動Camera
    * 若為hypriotOS須另外安裝raspi-config
    ```
     # start installing: 
     apt-get update && apt-get install -y alsa-utils

     #download raspi config: 
     wget http://archive.raspberrypi.org/debian/pool/main/r/raspi-config/raspi-config_20160108_all.deb

     #install raspi-config with:
     dpkg -i raspi-config_20160108_all.deb    
    ```
    > 參考：[Install # raspi-config on HypriotOS to activate Raspicam on Raspberry Pi1 & Pi2](https://www.youtube.com/watch?v=TEQE0A6VN6g)
    * 利用raspi-config指令開啟相機功能
    ```
    sudo raspi-confi
    # 接著會跳出圖形化介面，選擇 5 Interfacing Options >> P1 Camera
    # 接著重新開機後即可使用相機
    ```
    ![](/assets/螢幕截圖 2017-09-14 15.08.29.png)

* 簡易相機功能
 * 拍照
   * ```raspistill -o cam.jpg```
 * 錄影
   * ```raspivid -o vid.h264```
   
> 參考：https://www.raspberrypi.org/documentation/usage/camera/raspicam/