### Dynamic container deployment and resource monitoring mechanisms

---

Several existing open-source platforms and virtualization technologies may be leveraged to construct the fog computing platform. Our platform has to dynamically swap modules running on the devices. Such high dynamics results in several benefits: \(i\) we can quickly push a new module to a device, \(ii\) it is easy to update new algorithms as modules, and \(iii\) it is easy to migrate running modules to optimize the resource utilization or quality of service.

We selected Kubernetes to implement our fog computing platform, because it supports Docker, which is the latest and the most popular light-weight virtual machine.

#### Challenge

In highly programmable IoT platforms, the auto-deployment of containers need to consider the heterogeneities of hardware \(e.g., different CPU architectures, different sensors\). Furthermore, the GUI in the dashboards of container orchestration tools usually don’t provide data mixing both container cluster information and IoT device.

#### Solution

We proposed a mechanism that constructs images based on the deployment plan and deploys the resulting images over the network using Kubernetes. The mechanism also visualizes the current state of each node and detail informations of the IoT device by modifying Kubernetes UI Dashboard.

#### Ongoing work

Building and running unit tests for the prototype of auto-deployment mechanism.

