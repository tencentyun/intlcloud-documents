## Product Introduction

Container Instance Service (CIS) is a fully managed container service that hosts workloads using containers, and you don't need to manage and maintain servers. You can quickly deploy a batch of containers on the cloud with simple configurations, and schedule the pods on an existing Kubernetes cluster to CIS via the Kubernetes API to handle a sudden surge in your business. CIS can help you minimizes manual effort in OPS, and save costs by charging fees only for resources actually used by containers.

Similar to a Kubernetes Pod, a CIS instance can contain Dockers of multiple shared resources.

## Concepts

**Container and image**

By packaging all applications and their dependencies into an image, and then using the image to generate a resource-isolated environment to run the applications, the container technology allows applications to run independently in a consistent environment in a simple and efficient manner.

Container is a lightweight virtualization technology at the operating system level for isolating and controlling system resources, making global resources only usable in the container processes.

Similar to a CVM snapshot but more lightweight, a container image can be construed as a static form of a container. Image defines all files and dependencies needed to run a container, ensuring the container runs in a consistent manner.

**Kubernetes**

Kubernetes, an open source container orchestration and scheduling engine based on Google's Borg,
is one of the most important components of CNCF (Cloud Native Computing Foundation). It provides production-level application orchestration, container scheduling, service discovery, automatic scaling, and other capabilities. For more information, see [official Kubernetes documentation](https://kubernetes.io/docs/home).

## Product Features

**Rapidly deploy containers**

In just a few simple configuration steps, you can quickly deploy a container from an image without purchasing any CVM.

**Schedule and manage instances via Kubernetes**

CIS supports the [Virtual Kubelet](https://github.com/virtual-kubelet/virtual-kubelet) project. By deploying Virtual Kubelet on the nodes of the Kubernetes cluster, it can schedule container instances as the pods on this cluster.

**Communicate with other cloud resources**

CIS is running on your VPC and supports communicating with other resources on your VPC, including CVM, CDB, and CRS.

## Related Services

CIS can provide solutions together with other Tencent Cloud products.

For a better Kubernetes container management service, it is recommended to use [Kubernetes Service TKE](https://cloud.tencent.com/product/ccs).

To deploy different scenarios with CVMs and containers, it is recommended to use [CVM](https://cloud.tencent.com/product/cvm).

To manage more complex networks, such as establishing peering connections, using NAT gateways, configuring route tables or configuring security policies, it is recommended to use [VPC](https://cloud.tencent.com/product/vpc).

To call Tencent Cloud APIs to access Tencent Cloud products and services, see [Tencent Cloud API documentation](https://cloud.tencent.com/document/api).


