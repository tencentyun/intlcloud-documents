## Overview
Tencent Kubernetes Engine (TKE) is a container management service with high scalability and performance that enables you to easily run applications in a managed CVM instance cluster. This service frees you from installation, OPS, and expansion of the cluster management infrastructure. In addition, it allows you to launch and terminate Docker applications, query the status of clusters, and use various Tencent Cloud services through simple API calls. The containers can be arranged in your cluster based on the requirements of resources and availability to meet your business or application-specific needs.

Based on native Kubernetes, TKE is a container-oriented solution that solves operating environment issues during development, testing, and Ops and helps reduce costs and improve efficiency. It is fully compatible with the native Kubernetes APIs and extends Tencent Cloud's Kubernetes plugins such as Cloud Block Storage and Cloud Load Balancer. In addition, it leverages Tencent Cloud VPC to implement network solutions with high reliability and performance.

## Glossary
You will come across the following terms when using TKE:
- **Cluster**: This refers to the collection of cloud resources required for container operation, including several CVM instances, CLBs, and other Tencent Cloud resources.
- **Pod**: a Pod consists of one or more associated containers that share the same storage and network space.
- **Workload**: a Kubernetes resource object that is used to manage the creation, scheduling, and the automatic control of Pod replicas throughout the entire lifecycle.
- **Service**: refers to microservices consisting of multiple Pods of the same configuration and rule groups accessing those Pods.
- **Ingress**: a collection of rules for routing external HTTP(S) traffic to a Service.
- **Helm application**: a packaging tool for managing Kubernetes applications. It provides Helm Chart for visualized CRUD in specified clusters.
- **Image repository**: used to store Docker images which are used to deploy container services.


## Steps
As shown in the following figure, there are only three steps to run the application.
1. Create a cluster.
2. Create a workload or Ingress.
3. Run the Service or Ingress.

![][https://main.qcloudimg.com/raw/1a6296351069c4b8cad7e4362fa3415c.png]
## Pricing
TKE is now free of charge, but you need to pay for the usage of relevant Tencent Cloud resources. For more information on billing and pricing, see [Pricing Description](https://intl.cloud.tencent.com/document/product/457/6770).

## Relevant Services

- You can purchase several CVM instances to form a TKE cluster. The containers will run within the CVMs. For more information, see the [CVM documentation](https://intl.cloud.tencent.com/doc/product/213).
- A cluster can be created under a VPC. CVM instances in the cluster can be assigned to subnets in different availability zones. For more information, see the [VPC documentation](https://intl.cloud.tencent.com/doc/product/215).
- You can use CLB to automatically assign the request traffic of clients across CVM instances and then forward it to the containers running on the instances. For more information, see the [CLB documentation](https://intl.cloud.tencent.com/doc/product/214).
- Cloud Monitor can be used to monitor the operational statistics of TKE clusters and container pods. For more information, see the [Cloud Monitor documentation](https://intl.cloud.tencent.com/doc/product/248).




