##### 改 hypriotOS code

```
sudo vim /etc/kubernetes/kube-deploy/docker-multinode/common.sh

# line59
# IP_ADDRESS=${IP_ADDRESS:-${DEFAULT_IP_ADDRESS}}
IP_ADDRESS=asdfaklsdjflkasjdflj

# line177
# --etcd-endpoints=http://${MASTER_IP}:2379 \
--etcd-endpoints=http://${MASTER_IP}:4001 \

# line179
# --iface="${IP_ADDRESS}"
--iface=eth0

# line220
# --hostname-override=${IP_ADDRESS} \
--hostname-override=${hostname} \

# line247
# --hostname-override=${IP_ADDRESS} \
--hostname-override=${hostname} \
```