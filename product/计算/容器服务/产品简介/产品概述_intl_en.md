## Overview
Tencent Kubernetes Engine (TKE) is a container management service with high scalability and performance that enables you to easily run applications in a managed CVM instance cluster. It eliminates your need to install, operate, maintain, or expand the cluster management infrastructure. In addition, it allows you to enable/disable Docker applications, query status of clusters, and use various Tencent Cloud services through simple API calls. The containers can be arranged in your cluster based on the requirements of resources and availability to meet your business or application-specific needs.

Based on native Kubernetes, TKE is a container-oriented solution that solves operating environment issues during development, testing, and OPS and helps reduce costs and improve efficiency. It is fully compatible with the native Kubernetes APIs and extends Tencent Cloud's Kubernetes plugins such as CBS and CLB. In addition, it leverages Tencent Cloud VPC to implement network solutions with high reliability and performance.

## Glossary

You will come across the following terms when using TKE:
- **Cluster**: This refers to the collection of cloud resources required by container operation, including several CVM instances, load balancers, and other Tencent Cloud resources.
- **Application**: A complete application consists of one or more services and can be quickly deployed through templates.
- **Service**: This refers to microservices consisting of multiple Pods of the same configuration and rule groups accessing those Pods.
- **ConfigMap**: A ConfigMap is a collection of multiple configurations that help you manage different environments and services.
- **Ingress**: This is a collection of rules for routing external HTTP(S) traffic to a service.
- **Image repository**: This is used to store Docker images which are used to deploy container services.
- **Pod**: A pod consists of one or more associated containers that share the same storage and network space.

## Directions
You can run an application in the following three steps:
1. Create a cluster.
2. Create a service/application.
3. Run the service/application.

![][manual]

## Pricing
TKE is now free of charge, but you need to pay for the usage of relevant Tencent Cloud resources. For more information on billing and pricing, please see [TKE Pricing](https://intl.cloud.tencent.com/doc/product/457/6770).

## Related Services

- You can purchase several CVM instances to form a TKE cluster. The containers will run within the CVMs. For more information, see the [CVM documentation](https://intl.cloud.tencent.com/doc/product/213).
- A cluster can be created under a VPC. CVM instances in the cluster can be assigned to subnets in different availability zones. For more information, see the [VPC documentation](https://intl.cloud.tencent.com/doc/product/215).
- You can use CLB to automatically distribute the request traffic of clients across CVM instances and then forward it to the containers running on the instances. For more information, see the [CLB documentation](https://intl.cloud.tencent.com/doc/product/214).
- Cloud Monitoring can be used to monitor the operational statistics of TKE clusters and container pods. For more information, see the [Cloud Monitoring documentation](https://intl.cloud.tencent.com/doc/product/248).



[manual]:https://main.qcloudimg.com/raw/b21c1ca7d7013078a55d854a987c012a.png
