1. 準備一隨身碟至Ｍaster根目錄，壓縮根目錄下的些許檔案

```
＃ tar cvpzf [產出的備份檔路徑及名稱] --exclude=[排除的檔案或資料夾名稱]  /
$sudo su
$cd /
$sudo tar -cvpzf [隨身碟位址]/backup.tgz --exclude=/proc --exclude=/lost+found  --exclude=/mnt --exclude=/sys --exclude=/media --exclude=/dev  /
```

2. 在新電腦灌好ubuntu14.04

3. 在將隨身碟中的backup.tgz移至新電腦根目錄，並解壓縮

```
$sudo su
$cp [隨身碟位址]/backup.tgz /backup.tgz
$sudo tar -xvpfz ubuntu2015032801.tgz  -C /
$reboot
```

4. 裝之前使用apt-get 安裝的東西

```
$sudo apt-get systemd
```

5. 依照之前的方式安裝Docker 







