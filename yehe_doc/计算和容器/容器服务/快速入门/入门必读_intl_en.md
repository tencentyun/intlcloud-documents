
This document introduces the basics of Tencent Kubernetes Engine (TKE) and answers questions you may encounter when using TKE to help you quickly get started with TKE.


## Preparation
**Can I use TKE in a basic network?**
No. Currently, you can use TKE in a VPC instance but not a basic network.

## Simple Trial
- **How do I use TKE?**
Create a cluster and then create a service. For more information, see [Examples](https://intl.cloud.tencent.com/document/product/457/7851).

- **Can I add an existing CVM to a cluster?**
Yes. After a cluster is created, you can add existing CVMs to it.

- **Why does my service keep starting?**
If there is no process running in the container, the service may keep starting. For more information on service startup, see [Event FAQs](https://intl.cloud.tencent.com/document/product/457/8187).

- **How do I access a created service?**
Different access methods have different access entries. For more information, see [Service access methods](https://intl.cloud.tencent.com/document/product/457/30672).

- **How does a container access the public network?
If the host where the container resides has a public IP address and public network bandwidth, the container can access the public network directly. Otherwise, a NAT gateway is required for accessing the public network.

## Service Deployment
- **How do I manage configuration files or environment variables for my services?**
You can manage configuration files by editing [configuration items](https://intl.cloud.tencent.com/document/product/457/30675).

- **How do different services access one another?**
In a cluster, services with the same namespace can directly access one another, whereas services with different namespaces access one another by using <service-name\>.<namespace-name\>.svc.cluster.local.

- **What are the differences between ingress and "Public Network Access"?**
Ingress is a collection of rules to route external HTTP(S) traffic to services, and is not directly related to "Public Network Access".

- **Can my stateful service have a disk to rely on?**
Yes. You can mount data disks to a container by mounting CBS data volumes.

- **Will my service be interrupted when I run an update?**
No. Services can be updated in rolling update or quick update mode. Your service is not interrupted in rolling update mode.








