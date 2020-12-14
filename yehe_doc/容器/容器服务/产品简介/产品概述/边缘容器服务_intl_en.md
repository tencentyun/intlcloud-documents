## Product Introduction
Edge Cloud Kubernetes Engine (ECK) is a container system for managing edge cloud resources from a centralized cloud. ECK is fully compatible with native Kubernetes. You can manage nodes in multiple data centers with one cluster and deliver applications to all edge servers with one click. ECK also comes with edge autonomy and distributed health check features.


## Concepts

#### Containers and images
Containers are lightweight virtualization tools applied at the system level. With the ability to isolate and control system resources, containers restrict global resources access to processes in selected containers. A container image is a virtual machine snapshot and can be seen as the static form of a container. An image defines all files and dependencies required to run a container, ensuring consistency for running the container.

A container packages an application and its dependencies into an image, and then uses the image to generate a resource-isolated environment to run the application. This allows the application to run independently in a consistent environment in a simple and efficient manner.

#### Kubernetes
Kubernetes is an open-source Container Orchestration Engine (COE) inspired by a Google project called Borg. It is one of the most important components of the Cloud Native Computing Foundation (CNCF). Kubernetes provides production-level features such as application orchestration, container scheduling, service discovery, and autoscaling. For more information, see [Kubernetes Documentation](https://kubernetes.io/docs/home).

## Benefits of ECK

#### Native support
ECK is an out-of-the-box service that supports the latest Kubernetes version and native Kubernetes cluster management methods.


#### Availability across data centers
ECK is a Kubernetes service with master components hosted in the cloud and worker nodes located anywhere you want. Users do not need to provide resources required by the master components.

#### Security and reliability
ECK supports private and public network certificates separation and minimal node permissions to avoid cluster access leakage. TLS encryption is used in communication between the cloud and the edge to protect system management data from leakage and tampering.

#### System disaster recovery
ECK provides a reliable edge autonomy capability for cloud-edge communication scenarios. It also supports distributed cluster health check to help you determine the best time to migrate pods.

#### Easy system OPS
ECK leveraged Tencent’s years of experience in deep tunneling technologies to enable admins to log in to containers on edge servers directly from the cloud, even if the edge devices do not have public IP addresses.

#### Management across clouds
ECK supports management of public cloud, private cloud, Tencent Cloud, and any other cloud computing resources.

## Pricing

ECK is a Kubernetes service with master components hosted. Like TKE, ECK does not charge fees for management resources such as hosted control plane and Etcd.

Computing nodes are provided by users and therefore do not generate any additional charges.


## Use Cases

#### Edge computing
ECK helps you manage edge computing resources, allowing you to assign and schedule resources, deploy, upgrade and terminate applications, and perform system OPS from the cloud.

#### Management across clouds
With ECK, you can easily manage computing resources stored in various locations, form different cloud providers to your on-premises data centers, enjoying the convenience of centralized cloud management.


## Additional Services

For more information on how to call TencentCloud APIs to access Tencent Cloud products and services, see [TencentCloud APIs](https://intl.cloud.tencent.com/document/api).
