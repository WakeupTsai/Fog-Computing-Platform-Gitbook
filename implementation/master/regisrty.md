# Docker Resgistry

##### 1.Start your registry

$ docker run -d -p 5000:5000 --name registry registry:2

##### 2. View the images in the registry

$ curl 127.0.0.128:5000/v2/\_catalog 

{"repositories":\[\]} \#registry建立

##### 3. push images in registry

`$ docker pull wakeup706/tensorflow-audio  
 $ docker tag wakeup706/tensorflow-audio 127.0.0.128:5000/tensorflow-audio`



$ docker push 127.0.0.128:5000/tensorflow-audio \#images have pushed in registry



4. check if the images is inside the registry

$ curl 127.0.0.128:5000/v2/\_catalog 

{"repositories":\["tensorflow-audio"\]} \#registry建立









