## Overview
Tencent Kubernetes Engine (TKE) is a container management service with high scalability and performance that enables you to easily run applications in a managed CVM instance cluster. This service frees you from installation, OPS, and expansion of the cluster management infrastructure. In addition, it allows you to launch and terminate Docker applications, query the status of the cluster, and use various Tencent Cloud services through simple API calls. You can arrange containers in your cluster based on resource and availability requirements to meet your business or application-specific needs.

Based on native Kubernetes, TKE provides a container-oriented solution that solves operating environment issues during development, testing, and OPS and helps reduce costs and improve efficiency. It is fully compatible with the native Kubernetes APIs and extends Kubernetes plug-ins such as CBS and CLB on the Tencent Cloud. In addition, TKE provides network solutions with high reliability and performance based on Tencent Cloud VPC.

## Glossary
The following describes the key terms related to TKE:
- **Cluster**: the collection of cloud resources required to run containers, including several Tencent Cloud resources such as CVM instances and CLBs.
- **Pod**: a group of one or more associated containers that share the same storage and network space.
- **Workload**: a Kubernetes resource object that is used to manage the creation, scheduling, and the automatic control of Pod replicas throughout the entire lifecycle.
- **Service**: a group of microservices consisting of multiple Pods with the same configuration and the rules for accessing these Pods.
- **Ingress**: a collection of rules for routing external HTTP(S) traffic to a service.
- **Application**: features related to Helm 3.0 integrated in TKE, which provide you with various product and service capabilities including Helm Chart, Tencent Container Registry (TCR), and software services.
- **Image repository**: stores Docker images that are used to deploy TKE.


## Procedure
The following figure shows the TKE usage flowchart:
![](https://main.qcloudimg.com/raw/4a7b3a025c99e264eda78431ee964552.png)
1. Authorize roles.
   Sign up and log in to the TKE console and then grant permissions for your role to perform operations on relevant resources so that you can get started with TKE.
2. Create a cluster.
   You can customize a cluster or create a cluster from a template.
3. Deploy workloads.
   You can deploy workloads by deploying images or orchestrating the YAML file. For more information, see [Workloads](https://intl.cloud.tencent.com/document/product/457/30662).
4. Manage the lifecycle of Pods through operations such as monitoring, upgrade, and scaling.



## Pricing
TKE is now free of charge, but you need to pay for the usage of relevant Tencent Cloud resources. For more information on billing and pricing, see [Pricing Description](https://intl.cloud.tencent.com/document/product/457/6770).

## Relevant Services

- You can purchase several CVM instances to form a TKE cluster. The containers will run on the CVMs. For more information, see the [CVM Documentation](https://intl.cloud.tencent.com/document/product/213).
- A cluster can be created in a VPC. CVM instances in the cluster can be allocated to subnets in different availability zones. For more information, see the [VPC Documentation](https://intl.cloud.tencent.com/document/product/215).
- You can use CLB to automatically allocate the request traffic of clients across CVM instances and then forward it to the containers running on the CVM instances. For more information, see the [CLB Documentation](https://intl.cloud.tencent.com/document/product/214).
- You can use Cloud Monitor to monitor the operation statistics of TKE clusters and Pods. For more information, see the [Cloud Monitor Documentation](https://intl.cloud.tencent.com/document/product/248).




