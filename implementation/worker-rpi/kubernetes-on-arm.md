## kubernetes-on-arm
---
> https://github.com/luxas/kubernetes-on-arm/tree/v0.8.0

#### 燒錄SD卡
```
git clone https://github.com/luxas/kubernetes-on-arm
cd kubernetes-on-arm

# See which letter your newly inserted SD Card has:
sudo fdisk -l  # or lsblk

# Get some help text about supported options
sdcard/write.sh

# Template:
sudo sdcard/write.sh /dev/sdX [board] [os] [rootfs]

# Example
sudo sdcard/write.sh /dev/sdX rpi-3 hypriotos docker-multinode

# The installer will ask you if you want to erase all data on your card
# Answer y/n on that question
```

#### 改 hypriotOS code

```
sudo vim /etc/kubernetes/kube-deploy/docker-multinode/common.sh

# line59
# IP_ADDRESS=${IP_ADDRESS:-${DEFAULT_IP_ADDRESS}}
IP_ADDRESS=asdfaklsdjflkasjdflj
```
```
# line177
# --etcd-endpoints=http://${MASTER_IP}:2379 \
--etcd-endpoints=http://${MASTER_IP}:4001 \
```
```

# line179
# --iface="${IP_ADDRESS}"
--iface=eth0
```
```

# line220
# --hostname-override=${IP_ADDRESS} \
--hostname-override=${hostname} \
```
```

# line247
# --hostname-override=${IP_ADDRESS} \
--hostname-override=${hostname} \
```

#### 初始化並執行

```
# This script will install and setup docker etc.
kube-config install

# To set up your board as both a master and a node, run
kube-config enable-master

# To set up your board as a node, run
kube-config enable-worker [master-ip]
```