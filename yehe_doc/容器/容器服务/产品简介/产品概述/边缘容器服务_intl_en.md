## Product Introduction
Edge Cloud Kubernetes Engine (ECK) is a container system for managing edge cloud resources from the centralized cloud. ECK is fully compatible with native Kubernetes. It allows you to manage nodes in multiple data centers in one cluster and deliver applications to all edge servers at one click. It also enables edge autonomy and distributed health check.


## Concepts

#### Container and image
Container technology is a lightweight virtualization mechanism applied at the system level. With the ability to isolate and control system resources, it makes global resources available only to processes in containers. A container image is like a more lightweight virtual machine snapshot and can be seen as the static form of a container. An image defines all files and dependencies required to run a container, ensuring consistency for running the container.

A container packages an application and its dependencies into an image, and then uses the image to generate a resource-isolated environment to run the application. This allows the application to run independently in a consistent environment in a simple and efficient manner.

#### Kubernetes
Kubernetes is an open-source Container Orchestration Engine (COE) inspired by a Google project called Borg. It is one of the most important components of the Cloud Native Computing Foundation (CNCF). Kubernetes provides production-level features such as application orchestration, container scheduling, service discovery, and autoscaling. For more information, see [Kubernetes Documentation](https://kubernetes.io/docs/home).

## Benefits of ECK

#### Native support
ECK is an out-of-the-box service. It closely follows the community and supports the latest version of Kubernetes and the native Kubernetes cluster management methods.


#### Availability across data centers
ECK is a Kubernetes service with Master components hosted in the cloud and Worker nodes located anywhere. Users do not need to provide resources required by the Master components.

#### Security and reliability
ECK supports the separation of private network and public network certificates and minimal node permissions to avoid potential leakage of cluster access. TLS encryption is used in communication between the cloud and the edge to protect system management data from leakage and tampering.

#### System disaster recovery
ECK provides a reliable edge autonomy capability for cloud-edge communication scenarios. It also supports distributed cluster health check so that you can decide when is best to migrate pods.

#### Easy system OPS
With deep tunneling technologies accumulated by Tencent over the years, ECK allows admins to log in to containers on edge servers directly from the cloud, even if the edge devices do not have public IP addresses.

#### Management across clouds
ECK supports public cloud, private cloud, Tencent Cloud, and any other cloud computing resources.

## ECK Pricing

ECK is a Kubernetes service with Master components hosted. Like TKE, it does not charge you for management resources such as Master and Etcd.

Computing nodes are provided by users and therefore do not trigger any additional charges.


## Use Cases

#### Edge computing
ECK helps you manage computing resources at the edge, allowing you to assign and schedule resources, deploy, upgrade and terminate applications, and perform system OPS from the cloud.

#### Management across clouds
With ECK, you can manage computing resources located in different locations, managed by multiple cloud providers, or stored in your on-premises data centers from one place, enjoying the convenience of centralized cloud management.


## Relevant Services

For more information on how to call TencentCloud APIs to access Tencent Cloud products and services, see [TencentCloud APIs](https://intl.cloud.tencent.com/document/api).
