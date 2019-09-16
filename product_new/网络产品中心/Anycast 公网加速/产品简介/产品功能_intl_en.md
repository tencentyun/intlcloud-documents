## Overview
Tencent Cloud Anycast Internet Acceleration can help customers perform EIP Anycast in multiple regions, thereby achieving the following features:
### Same Server in Multiple Regions
All of users' requests and responses can come in and out from the nearest Tencent Cloud API, and only one service cluster, one database or one storage node needs to be deployed at the backend. After IP Anycast is performed, the backend service will be available in multiple regions through Tencent Cloud's private network-based Direct Connect. However, in traditional mode, only one cluster or one storage node is deployed in each region to serve nearby customers.
### Multi-regional Acceleration
Slow connection to the internet can be avoided, and services are not affected by the congestion on the internet, north-south issue, and ISP's failures.
### Avoiding Congestion
Based on the capabilities of Anycast, the congestion can be avoided during the internet transmission.
![](https://main.qcloudimg.com/raw/1783f606087ffc8b326e1d55a2073a8b.png)

### Blocking Failures
Since the internet ISP's network fails from time to time, Anycast is capable to block the failures.
![](https://main.qcloudimg.com/raw/6b22d2ec9758fd325e2f114377feec59.png)
## Further Reading
**The following concepts can help you understand AIA:**
For more information on the concepts, see [Glossary](https://intl.cloud.tencent.com/document/product/644/12625).
**To provide Anycast service, public cloud vendors must have a powerful network for interconnecting nodes worldwide, as well as the capability of cross-region network scheduling. The basic capabilities of AIA are as follows:**

- Multi-path ISP aggregation: Tencent Cloud has TB-level BGP network egress with 35+ ISP lines.
- Multi-node interconnection: Tencent Cloud's global TB-level backbone network is used for hosting.
- Multi-dimensional network monitoring models, global network monitoring alarms, and real-time detections of internet conditions.
- SDN controller that controls the entire network can change IP publishing sites in seconds and enable multidimensional and fine-grained control.
- Optimal path algorithm is generated through self-learning.
