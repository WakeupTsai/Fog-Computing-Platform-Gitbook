# Fog Computing Platform

---
The Internet of Things \(IoT\) is getting popular all over the world. There are 6.4 billion IoT devices deployed in 2016, which is 30% more compared to 2015, and the number is expected to increase to 20.8 billion in 2020. Currently, the devices are used to sense/collect data and send the data to powerful servers, such as cloud servers through the Internet for processing and further analysis. After that, the analyzed results are sent to IoT users for various IoT applications, such as smart cities, smart homes, and smart hospitals.

The incredible growing speed of the number of IoT devices leads to many problems, they generate huge amount of data which causes seriously resource shortage. For instance, severe network congestion and surging server loads under the huge amount of incoming data streams generated by many IoT devices.That make users can not get the results in time and reduce the user experience. In addition, the current application of the Internet of Things does not have a unified platform for development, for example, smart home and the smart healthcare are two independent systems, which led to the development problems. Communicate between the IoT system also becomes challenge.

In this project, we implement an unified IoT platform which can dynamically replace the applications or algorithms on IoT devices, manage and monitor the resource on devices, and analyze the information to improve the platform performance. We use the idea of Fog Computing to build this IoT platform. Fog computing leverages fog devices in data centers, edge networks, and end devices simultaneously. The fog devices \(minions\) are managed by a centralized server \(master\). The heterogeneous fog devices help us to pre-process the data on the resource-limited devices, including the edge networks and end devices. Moreover, the fog computing platform extends cloud to end devices, which are closer to end users, and result in lower latency

We use the street lights as an example of IoT devices, there are thousands of street lights all over the city. Regard those street lights as Minion and put variety of devices on them, such as temperature sensor, air pollution sensor, camera, or a single board computer for data sensing, storage, computing, and sent data to the cloud for analysis. To send those incredible amount of data to the cloud server, it is challenge to build an efficient network topology. For instance, let all Minions transmit the data through 4G network will very expensive. Finally, the data will be uploaded to the cloud server for further analysis. The results of the analysis can be presented visually to the user and can also be used to improve the overall system.



