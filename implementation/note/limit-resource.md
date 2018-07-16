### 限制Namespace中所有pods 資源

1. limit.yaml

```
kind: LimitRange
metadata:
  name: mylimits
spec:
  limits:
  - max:
      cpu: "2"
      memory: 1Gi
    min:
      cpu: 200m
      memory: 6Mi
    type: Pod

  - default:
      cpu: 300m
      memory: 200Mi
    defaultRequest:
      cpu: 200m
      memory: 100Mi
    max:
      cpu: "2"
      memory: 1Gi
    min:
      cpu: 100m
      memory: 3Mi
    type: Container
```

2. deploy limit.yaml 去限制該namespace中的各服務之資源

```
kubectl create -f limit.yaml --namespace=example
```

### 從yaml檔限制運算資源

```
spec:
  containers:
  - name: co2-sensor
    imagePullPolicy: Always
    image: little170/scalebox:co2 
    resources:
      limits:
        cpu: "1"
        memory: 512Mi
      requests:
        cpu: "1"
        memory: 512Mi

```



