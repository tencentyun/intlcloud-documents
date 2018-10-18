### **How does CIS ensure security?**

The network environment where CIS runs is a user-defined private network, and the network layer has been logically isolated from other users. It also allows users to configure security groups and network ACL to limit traffic. Security groups can be used to specify inbound and outbound network traffic to and from various CVMs. Traffic which is not explicitly allowed to or from an instance is automatically denied. Access Control List (ACL) can also allow or deny the network traffic to and from each subnet.
CIS's underlying resources are isolated at the CVM level. In addition, Tencent Cloud team uses the accumulated massive threat data for machine learning to provide security protection such as hacker intrusion detection and vulnerability risk alert for the underlying servers.

### **What scenarios does CIS apply to?**

It is suitable for lightweight and small applications or distributed systems that do not need to run for a long term in a sustained and stable manner nor require complex upper-level management. For example, building a test environment, DevOps process, agent program, crawler, offline computing, batch data processing, etc.


