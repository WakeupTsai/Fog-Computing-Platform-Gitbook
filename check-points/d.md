### Monitor fog network conditions using software-defined networks

---

To achieve the goal of dynamic deployment on our fog platform, the master and each device have to know the exact target address every time on their own when sending message and push containers. Thus, we need software-defined networks \(SDN\) to provide a programmable network environment. Namely,  we can run programs to automatically control the network behavior among the master and devices.

We select OpenContrail and OpenStack, which are both open-source and widely used softwares for SDN and cloud computing, to automatically control the network behavior on our fog platform.

#### Challenge

The first challenge of SDN is to make sure that OpenContrail and OpenStack can perform on our fog platform. To be pricise, OpenContrail and OpenStack can exactly control the OpenFlow on our fog platform. Morever, we want to write the programs to exactly and automatically control the network behavior on our fog platform.

#### Solution

We want to firstly integrate OpenContrail and OpenStack to our platform by reading their source code and changing some setting of them and our platform. In the next step we will tries to define the network behavior according our algorithm.

