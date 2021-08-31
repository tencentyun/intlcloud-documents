
## How It Works
VPC-CNI is a container network capability provided by TKE based on CNIs and VPC ENIs. It is suitable for scenarios with high latency requirements. In this network mode, containers and nodes are located on the same network plane, and container IP addresses are ENI IP addresses assigned by the IPAMD component.


VPC-CNI has a shared ENI mode and an exclusive ENI mode. The two network modes are suitable for different scenarios. You can select a network mode based on your business needs.
- [Shared ENI Mode](https://intl.cloud.tencent.com/document/product/457/38971): Pods share an ENI, and the IPAMD component applies multiple IPs for the ENI to different Pods. It supports static pod IP addresses. For details, see [Static IP Address Usage](https://intl.cloud.tencent.com/document/product/457/38975).
- [Exclusive ENI Mode](https://intl.cloud.tencent.com/document/product/457/38972): each Pod has an independent ENI, which can provides a higher performance. Due to the limitation of model, the number of ENIs that available for different nodes is limited and the Pod density of a single node is lower.


## Use limits

- Subnets in VPC-CNI mode cannot be used by other cloud resources, such as CVMs and CLBs.
- The nodes in the cluster need to be in the same AZ as the subnet, otherwise, the Pod cannot be scheduled.
- The number of pods that can be scheduled in VPC-CNI mode on a node is limited by the maximum number of IP addresses that can be bound with the inserted ENIs. Devices with higher configurations allow the insertion of more ENIs. You can check the Allocatable attribute of the node to confirm the number of ENIs that can be inserted.


## Use Cases

Compared with Global Router, the advantages and applicable scenarios of VPC-CNI are as follows:

- Without the need for a network bridge, the network forwarding performance is enhanced by about 10%. This mode is suitable for scenarios with high network latency requirements.
- It supports static pod IP addresses. This mode is suitable for scenarios that rely on static container IP addresses. For example, migration from a traditional architecture to a container platform and security policy restrictions on IP addresses.
- It supports LB-to-Pod direct connection.


