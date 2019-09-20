## Overview
Tencent Cloud Anycast Internet Acceleration can help customers perform EIP Anycast in multiple regions, thereby achieving the following features:
### Same Server in Multiple Regions
All of users' requests and responses can come in and out from the nearest Tencent Cloud API, and only one service cluster, one database or one storage node needs to be deployed at the backend. After IP Anycast is performed, the backend service will be available in multiple regions through Tencent Cloud's private network-based Direct Connect. However, in traditional mode, only one cluster or one storage node is deployed in each region to serve nearby customers.
### Multi-regional Acceleration
Avoid slow connection to the internet – services are not affected by the congestion on the Internet, cross-carrier issue, and ISPs’ failures.
### Avoiding Congestion
Anycast is capable of avoiding the Internet congestion.
![](https://main.qcloudimg.com/raw/52f9dbf12a2dfa4edb05581a4f2473c0.png)

### Blocking Failures
Since the internet ISPs’ networks fail from time to time, Anycast is capable to block the failures.
![](https://main.qcloudimg.com/raw/67d339bb1257493017569af60b28c6d0.png)
## Further Reading
**The following concepts can help you understand AIA:**
For more information on the concepts, see [Glossary](https://intl.cloud.tencent.com/document/product/644/12625).
**To provide Anycast service, public cloud vendors must have a powerful network for interconnecting nodes worldwide, as well as the capability of cross-region network scheduling. The basic capabilities of AIA are as follows:**

- Multi-path ISP aggregation: Tencent Cloud has TB-level BGP network egress with 35+ ISP lines.
- Multi-node interconnection: Tencent Cloud's global TB-level backbone network is used for hosting.
- Multi-dimensional network monitoring models, global network monitoring alarms, and real-time detections of internet conditions.
- SDN controller that controls the entire network can change IP publishing sites in seconds and enable multidimensional and fine-grained control.
- Optimal path algorithm is generated through self-learning.
