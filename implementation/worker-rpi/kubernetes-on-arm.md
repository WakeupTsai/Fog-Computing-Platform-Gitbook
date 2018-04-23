## kubernetes-on-arm

---

> [https://github.com/luxas/kubernetes-on-arm/tree/v0.8.0](https://github.com/luxas/kubernetes-on-arm/tree/v0.8.0)

#### 燒錄SD卡

```
git clone https://github.com/luxas/kubernetes-on-arm
cd kubernetes-on-arm

# See which letter your newly inserted SD Card has:
sudo fdisk -l  # or lsblk

# Format sd card
sudo umount /dev/sdX
sudo mkfs.vfat /dev/sdX -I

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

#### 問題

* ##### Cannot connect to the Docker daemon. Is the docker daemon running on this host?

```
sudo nohup docker daemon -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock &
sudo usermod -aG docker <username>

參考：https://forums.docker.com/t/cannot-connect-to-the-docker-daemon-is-the-docker-daemon-running-on-this-host/8925
參考：https://www.upcloud.com/support/how-to-configure-docker-swarm/
```



