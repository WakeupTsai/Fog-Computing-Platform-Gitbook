# Docker Resgistry

##### 1.Start your registry

`$ docker run -d -p 5000:5000 --name registry registry:2`

##### 2. View the images in the registry

```
$ curl 127.0.0.128:5000/v2/_catalog
{"repositories":[]}
```

##### 3. push images in registry

```
$ docker pull wakeup706/tensorflow-audio    
$ docker tag wakeup706/tensorflow-audio 127.0.0.128:5000/tensorflow-audio
$ docker push 127.0.0.128:5000/tensorflow-audio #images have pushed in registry
```

##### 4. check if the images is inside the registry

```
$ curl 127.0.0.128:5000/v2/_catalog
{"repositories":["tensorflow-audio"]}
```

##### 5. Pull the images from registry



```
$ docker pull 127.0.0.128:5000/tensorflow-audio
```

這裡可能遇到“registry pull fail: server gave HTTP response to HTTPS client” 問題

```
＃Create or modify /etc/docker/daemon.json
{ "insecure-registries":["127.0.0.128:5000"] }

＃Restart docker daemon
＄ sudo /etc/init.d/docker restart
```



