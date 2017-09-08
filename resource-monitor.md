## Resource Monitor
---
It is important to keep monitoring the resources usage of each fog devices,this can help us make a more reasonable deployment when take these factors into account.Kubernetes has an extension named heapster which enables container cluster monitoring and performance analysis. And we improve this extension by adding network monitoring and sensors monitoring. After that we proposed an algorithm which takes this information into account and then calculate the best way to deploy the modules through Kubernetes. And we also improve another extension of Kubernetes named Kubernetes dashboard to let users see those information conveniently.
##### Challenge
The orginal Kubernetes can only send some  resource information defined by hard code, for example, CPU and memory usage. If we want to know more information about the fog device, for example, the location of the fog device, we need to modify the source code to manage the additional sensors we add to the fog device and send these information to the master so that we can manage the cluster and deploy modules based on these information. 
##### Solution 
Read Kubernetes source code related to Resource Monitor, know how kubernetes monitor the resource and add more function into it to make our platform able to monitor more resource and send these information to master. 
##### Ongoing work
Modifing the source code to send the location of the fog device to the master.