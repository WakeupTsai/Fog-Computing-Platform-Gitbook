# Tensorflow

---

### tensorflow on PI
- https://github.com/samjabrahams/tensorflow-on-raspberry-pi


### virtualenv新建python環境

```
# 建立
virtualenv —system-site-packages targetDirectory
# 或者指定版本
virtualenv -p /usr/bin/python2.6 <path/to/new/virtualenv/>
# python3
virtualenv -p python3  <path/to/new/virtualenv/>

#進入環境
source targetDirectory/bin/activate

#離開
deactivate
```

### tensorboard
- http://darren1231.pixnet.net/blog/post/333059241-tensorflow教學----可視化tensorboard
```
    # 在程式尾端加上
    writer = tf.summary.FileWriter("logs/", sess.graph)

    # 將存好的log已網頁版tensorboard開啟
    tensorboard --logdir='logs/'	
```

### 筆記

- 不顯示某些error
```export TF_CPP_MIN_LOG_LEVEL=2```



