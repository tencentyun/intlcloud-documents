

## Overview
Tencent Kubernetes Engine (TKE) is a container management service with high scalability and performance that enables you to easily run applications in a managed CVM instance cluster. This service frees you from installation, operations, and expansion of the cluster management infrastructure. In addition, it allows you to launch and terminate Docker applications, query the status of the cluster, and use various Tencent Cloud services through simple API calls. You can arrange containers in your cluster based on resource and availability requirements to meet your business or application-specific needs.

Based on native Kubernetes, TKE provides a container-oriented solution that solves operating environment issues during development, testing, and OPS and helps reduce costs and improve efficiency. TKE is fully compatible with the native Kubernetes APIs and extends Kubernetes plug-ins such as CBS and CLB on the Tencent Cloud. In addition, TKE provides network solutions with high reliability and performance based on Tencent Cloud VPC.



## Glossary
The following describes the key terms related to TKE:
- **Cluster**: The collection of cloud resources required to run containers, including several Tencent Cloud resources such as CVM instances and CLBs.
- **Pod**: A group of one or more associated containers that share the same storage and network space.
- **Workload**: A Kubernetes resource object that is used to manage the creation, scheduling, and the automatic control of Pod replicas throughout the entire lifecycle.
- **Service**: A group of microservices consisting of multiple Pods with the same configuration and the rules for accessing these Pods.
- **Ingress**: A collection of rules for routing external HTTP(S) traffic to a service.
- **Application**: The features related to Helm 3.0 that are integrated in TKE. They enable you to create products and services such as Helm Chart, container images, and software services.
- **Image repository**: It stores Docker images that are used to deploy TKE.


## Directions
The procedure to use TKE:
![](https://main.qcloudimg.com/raw/4a7b3a025c99e264eda78431ee964552.png)

1. Authorize roles.
   Register and log in to the [TKE console](https://console.cloud.tencent.com/tke2), complete service authorization to obtain operation permissions for relevant resources.
2. Create a cluster.
   You can customize a cluster or create a cluster with a template.
3. Deploy workloads.
   You can deploy workloads by deploying images or orchestrating the YAML file. For more information, see [Workload](https://intl.cloud.tencent.com/document/product/457/30661).
4. Manage the lifecycle of Pods through operations such as monitoring, upgrade, and scaling.



## Pricing
TKE charges cluster management fees based on the specifications of the managed clusters, and charges cloud resources fees based on the actual usage. For more information about the billing modes and prices, see [TKE Billing Overview](https://intl.cloud.tencent.com/document/product/457/45157).

## Additional Services

- You can purchase several CVM instances to form a TKE cluster. The containers will run on the CVMs. For more information, see the [CVM Documentation](https://intl.cloud.tencent.com/document/product/213).
- A cluster can be created in a VPC. CVM instances in the cluster can be allocated to subnets in different availability zones. For more information, see the [VPC Documentation](https://intl.cloud.tencent.com/document/product/215).
- You can use CLB to automatically allocate the request traffic of clients across CVM instances and then forward it to the containers running on the CVM instances. For more information, see the [CLB Documentation](https://intl.cloud.tencent.com/document/product/214).
- You can use Cloud Monitor to monitor the operation statistics of TKE clusters and Pods. For more information, see the [Cloud Monitor Documentation](https://intl.cloud.tencent.com/document/product/248).



