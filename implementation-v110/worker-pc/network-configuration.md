## Static IP

1.修改/etc/netplan/50-cloud-init.yaml

```
vim /etc/netplan/50-cloud-init.yaml
```

2. example

```
network:
    ethernets:
        eth0:
            addresses:
            - 192.168.0.100/24
            gateway4: 192.168.0.254
            nameservers:
                addresses:
                - 8.8.8.8
                search: []
            optional: true
        eth1:
            addresses:
            - 192.168.0.99/24
            optional: true
    version: 2
```

3. apply netplan

```
sudo netplan apply
```

## Wifi

1.使用nuclei 即可！

```
sudo nmcli wifi connect <wifi-ap> password <passwd>
```

2.將此指令加到rc.local service 

```
ln -fs /lib/systemd/system/rc-local.service /etc/systemd/system/rc-local.service

cd /etc/systemd/system/
vim rc-local.service
```

3. example of rc-local.service

```
[Unit]
 Description=/etc/rc.local Compatibility
 ConditionPathExists=/etc/rc.local
 
[Service]
 Type=forking
 ExecStart=/etc/rc.local start
 TimeoutSec=0
 StandardOutput=tty
 RemainAfterExit=yes
 SysVStartPriority=99
 
[Install]
 WantedBy=multi-user.target
```

4.更改rc.local權限

```
chmod 755 /etc/rc.local
```

5.將指令加到/etc/rc.local

```
#!/bin/bash
nmcli wifi connect <wifi-ap> password <passwd>
```



