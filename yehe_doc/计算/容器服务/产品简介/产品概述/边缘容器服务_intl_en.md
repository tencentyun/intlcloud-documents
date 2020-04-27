## Product Introduction
Tencent Kubernetes Engine for Edge (TKE Edge) is a container system for managing edge cloud resources from the center of the cloud. TKE Edge is fully compatible with native Kubernetes. It allows you to manage nodes in multiple data centers in the same cluster and deliver applications to all edge servers with one click. It also enables edge autonomy and distributed health check.
>To use TKE Edge, [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for it.
>

## Concepts

#### Containers and images
Container technology is a lightweight virtualization mechanism applied at the system level. With the ability to isolate and control system resources, it makes global resources available only to processes in containers. A container image is like a more lightweight virtual machine snapshot and can be seen as the static form of a container. An image defines all files and dependencies required to run a container, ensuring consistency for running the container.

A container packages an application and its dependencies into an image, and then uses the image to generate a resource-isolated environment to run the application. This allows the application to run independently in a consistent environment in a simple and efficient manner.

#### Kubernetes
Kubernetes is an open-source Container Orchestration Engine (COE) inspired by a Google project called Borg. It is one of the most important components of the Cloud Native Computing Foundation (CNCF). Kubernetes provides production-level features such as application orchestration, container scheduling, service discovery, and autoscaling. For more information, see [Kubernetes Documentation](https://kubernetes.io/docs/home).

## Benefits of TKE Edge

#### Native support
TKE Edge is an out-of-the-box service. It develops in line with the community and supports the latest version of Kubernetes and native Kubernetes cluster management methods.


#### Availability across data centers
TKE Edge is a Kubernetes service with Master components hosted in the cloud and Worker nodes located anywhere. Users do not need to provide resources required by the Master components.

#### Security and reliability
TKE Edge supports the separation of private network and public network certificates and minimal node permissions to avoid potential leakage of cluster access. TLS encryption is used in communication between the cloud and the edge to protect system management data from leakage and tampering.

#### System disaster recovery
TKE Edge provides a reliable edge autonomy capability for cloud-edge communication scenarios. It also supports distributed cluster health check so that you can decide when is best to migrate pods.

#### Easy system OPS
With the extensive tunneling technologies accumulated by Tencent over the years, TKE Edge allows admins to log in to containers on edge servers directly from the cloud, even if the edge devices do not have public IP addresses.

#### Management across clouds
TKE Edge supports public cloud, private cloud, Tencent Cloud, and other cloud computing resources.

## TKE Edge Pricing

TKE Edge is a Kubernetes service with Master components hosted. Like TKE-managed clusters, it does not charge you for management resources such as Master and Etcd.

Computing nodes are provided by users and therefore do not incur any additional charges.


## Application Scenarios

#### Edge computing
TKE Edge helps you manage computing resources at the edge, allowing you to assign and schedule resources, deploy, upgrade and terminate applications, and perform system OPS from the cloud.

#### Management across clouds
With TKE Edge, you can manage computing resources located in different locations, managed by multiple cloud providers, or stored in your on-premises data centers from one place, enjoying the convenience of centralized cloud management.


## Related Services

For more information on how to call Tencent Cloud APIs to access Tencent Cloud products and services, see [Tencent Cloud APIs](https://intl.cloud.tencent.com/document/api).
