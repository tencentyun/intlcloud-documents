## Overview
Elastic Kubernetes Service (EKS) is a TKE service mode that allows you to deploy workloads without purchasing any nodes. EKS is fully compatible with native Kubernetes, allowing you to purchase and manage resources natively. This service is billed based on the actual amount of resources used by containers. In addition, EKS provides extended support for Tencent Cloud products, such as storage and network products, and can ensure the secure isolation of containers. EKS is ready to use out-of-the-box.


## Concepts
#### Containers and images
Containers are virtualization tools applied at the process level. With the ability to isolate and control system resources, containers restrict global resources access to processes in selected containers. A container image is a virtual machine snapshot and can be seen as the static form of a container. An image defines all files and dependencies required to run a container, ensuring consistency for running the container.
By containerization, all applications and their dependencies are packaged into an image, and then use the image to generate a resource-isolated environment to run the applications. This allows the applications to run independently in a consistent environment in a simple and efficient manner.

#### Kubernetes
Kubernetes is an open-source Container Orchestration Engine (COE) inspired by a Google project called Borg. It is one of the most important components of the Cloud Native Computing Foundation (CNCF). Kubernetes provides production-level features such as application orchestration, container scheduling, service discovery, and autoscaling. For more information, see [Kubernetes Documentation](https://kubernetes.io/docs/home).

## Strengths
#### Native support
EKS is community-driven and supports the latest version of Kubernetes and native Kubernetes cluster management. It serves as a plug-in to provide extended support for Tencent Cloud products, such as storage, network, and load balancing products. EKS is ready to use out-of-the-box.

#### Serverless
EKS is a fully-managed Kubernetes service, which means that you do not need to manage any computing nodes. EKS delivers computing resources by using Pods. It allows you to purchase, return, and manage cloud resources as in Kubernetes.

#### High security and reliability
EKS can achieve 99.95% or higher availability based on the mature virtualization technology and network architecture of Tencent Cloud. Tencent Cloud ensures virtual isolation and network isolation between the EKS clusters of different users and allows users to configure network policies for a specific service by using services such as security groups and network Access Control List (ACL).

#### Scaling within seconds
With the lightweight virtual technology developed by Tencent Cloud, you can create or delete a TKE instance within seconds to ensure higher efficiency when creating resources. EKS allows you to configure the native Horizontal Pod Autoscaler (HPA) of Kubernetes so that services can be automatically scaled based on actual loads.

#### Reduced costs
The serverless architecture allows EKS to provide higher resource utilization and lower OPS costs. The flexible and efficient auto scaling capability ensures that EKS only consumes the amount of resources required by the current load.

#### Service integration
EKS can be highly integrated with most Tencent Cloud services, including the storage products Cloud Block Storage (CBS), Cloud File Storage (CFS), and Cloud Object Storage (COS), TencentDB product family, and virtual private cloud (VPC) product family. With this capability, EKS can provide solutions that meet the requirements of a wide range of businesses.

## Use Limits
- For more information, see [Purchase Limits](https://intl.cloud.tencent.com/document/product/457/34056).

## Pricing
EKS is a fully-managed and serverless Kubernetes service. Managed control-plane resources such as the Master and Etcd are not billed in an elastic cluster. This billing method is similar to that of a TKE-managed cluster. Workloads running in an elastic cluster are billed in pay-as-you-go mode. The fees are calculated based on the configured amount of resources and the actual use period. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/457/34055).


## Comparison with TKE
<table>
<thead>
<tr>
<th>Feature</th>
<th>TKE</th>
<th width="47%">EKS</th>
</tr>
</thead>
<tbody><tr>
<td>Kubernetes</td>
<td>This feature is natively supported.</td>
<td>This feature is natively supported. Some features are not supported due to the lack of computing nodes. For more information, see <a href="https://intl.cloud.tencent.com/document/product/457/34050">Unsupported Features</a>.</td>
</tr>
<tr>
<td>VPC</td>
<td colspan=2>This feature is supported.</td>
</tr>
<tr>
<td>Computing nodes</td>
<td>You need to purchase and manage computing nodes such as Cloud Virtual Machine (CVM) and Bare Metal (BM) nodes on your own.</td>
<td>You do not need to purchase any computing nodes.</td>
</tr>
<tr>
<td>Management method</td>
<td colspan=2>Native Kubernetes APIs and Kubectl are supported.</td>
</tr>
<tr>
<td>Clusters</td>
<td colspan=2>Multiple clusters can be created and managed.</td>
</tr>
<tr>
<td>Namespaces</td>
<td colspan=2>This feature is natively supported.</td>
</tr>
<tr>
<td>Workloads</td>
<td>This feature is natively supported.</td>
<td>Native Kubernetes workloads, except DaemonSet, are supported.</td>
</tr>
<tr>
<td>Services</td>
<td colspan=2>This feature is natively supported. A CLB plug-in is integrated with TKE.</td>
</tr>
<tr>
<td>Storage</td>
<td colspan=2>This feature is natively supported. Plug-ins such as CBS and CFS can be integrated with TKE.</td>
</tr>
</tbody></table>

## Use Cases
#### Microservices
Running microservices with EKS can free users from OPS of computing nodes. A service can be automatically scaled based on the actual load, and the necessary amount of resources is used to run applications, which reduces resource costs.

#### Offline computing
To run an offline computing task with EKS, you simply need to prepare a container image to quickly deploy workloads for the task. In addition, EKS bills only the actual amount of computing resources used during the execution of the task and stops billing when pods are automatically released after the task ends.

#### Online inference
EKS can run online inference services by using CPU, GPU, and vGPU resources. The abundant resource specifications and the workloads that support autoscaling improve the operating efficiency and cost-effectiveness of the online inference services.

## Additional Services
- Storage: To use a cloud disk or file storage as the persistent storage of a container, you can use [CBS](https://intl.cloud.tencent.com/product/cbs) or [CFS](https://intl.cloud.tencent.com/product/cfs).
- Network:
 - To create and manage your private network, including to create a VPC instance and a subnet, establish a peering connection, use the NAT Gateway, configure a route table, or configure a security policy, please refer to the [VPC documentation](https://intl.cloud.tencent.com/product/vpc).
 - To manage service access configurations for private and public network traffic, you can use [CLB](https://intl.cloud.tencent.com/product/clb).
- APIs: To gain access to Tencent Cloud products and services by calling Tencent Cloud APIs, refer to the [Tencent Cloud API documentation](https://intl.cloud.tencent.com/document/api).


