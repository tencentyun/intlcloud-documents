This ducument is designed to help you understand the Tencent Kubernetes Engine (TKE), to answer any questions you may encounter when using TKE, and to help you get started using TKE faster.

## Preparation for Use

Can I use TKE on a basic network?
No. Currently, TKE only supports VPC networks, and does not support basic networks.

## Simple Trial

1. How do I use TKE?
   There’re only two steps, creating a cluster, and then creating services. For more information, see [Getting Started Examples](https://intl.cloud.tencent.com/document/product/457/7851).
2. Can I add an existing CVM to the cluster?
   Yes. After a cluster is created, you can add existing CVMs to it.
3. Why does my service keep starting?
   If the container in the service does not have continuous running processes, this will cause the service to always be in startup. For more information about service startup issues, see [Event-related FAQs](https://intl.cloud.tencent.com/document/product/457/8187).
4. How do I access created Services?
   Different access points are provided for different access methods. For more information, see [Service Access Modes](https://intl.cloud.tencent.com/document/product/457/9098).
5. How does the container access the public network?
   If the node where the container resides has a public network IP and bandwidth, the container can directly access the public network. Otherwise, an NAT gateway is required for accessing the public network.

## Deploying Projects

1. My project needs to configure a lot of text or environment variables. How do I manage them?
   You can use [Configuration Items](https://intl.cloud.tencent.com/document/product/457/10173) to manage config files.
2. How do services access each other?
   In a cluster, services with the same namespace can directly access each other. Services with different namespaces need to use <service-name\>.<namespace-name\>.svc.cluster.local to access each other.
3. What are the differences between **ingress** and the service access method of **public network access**?
   Ingress is a collection of rules used to route external HTTP(S) traffic to service, which is not directly related to the service access method of **public network access**.
4. My project is stateful and needs to reply on a disk. Can I access it with TKE?
   You can mount data disks to containers in the form of CBS data volumes.
5. Will my project be interrupted when the service is updating?
   There are two ways to update services: rolling updates and rapid updates. Select rolling update to not interrupt your project.







