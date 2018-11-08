# Docker Registry Managed by K8s

* create docker registry

```
kubectl create secret docker-registry registrykey-m2-1 --docker-server=registry.cn-hangzhou.aliyuncs.com/xxxx/rbd-rest-api --docker-username={username} --docker-password={password} --docker-email={mail}
```

* pull and push



