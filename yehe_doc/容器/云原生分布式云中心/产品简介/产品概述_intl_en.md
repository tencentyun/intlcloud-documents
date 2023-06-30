## Overview

Tencent Kubernetes Engine Distributed Cloud Center is an application management platform for multi-cloud and multi-cluster scenarios. Users can expand the cloud-native applications to distributed cloud, and manage and operate the distributed cloud resources in a unified way from a global respective.

Tencent Kubernetes Engine Distributed Cloud Center interconnects public cloud, private cloud and edge cloud, delivers public cloud products and services including mature clusters, networks, storage, microservices and operations to locations that are closer to users. It ensures unified control plane under different cloud infrastructures, and provides reliability and conformance guarantees to meet the requirements of enterprises for multi-cloud management, application governance and high-availability disaster recovery.

Source code of core features in Tencent Kubernetes Engine Distributed Cloud Center have been provided for public use. Vendors and customers can use the source code to build their own container application platforms.

- [Clusternet](https://github.com/clusternet/clusternet) multi-cluster application governance project
- [TKEStack](https://github.com/tkestack/tke) open-source TKE platform


## Features

**Infrastructure management**

You can easily manage massive Kubernetes clusters. No matter they are running on public cloud, private cloud, hybrid cloud or edge cloud, you can manage and access them just like they are running locally, and centrally deploy and coordinate multi-cluster applications and services through standard APIs.

**Distributed application management**

Tencent Kubernetes Engine Distributed Cloud Center uses a distributed application management model based on cloud-native design. It expands native K8s resources to multiple cloud and multiple clusters, supports distributing various resources to different clusters, including Kubernetes native Deployment/StatefulSet/ConfigMap/Secret, custom CRDs and third-party CRD resources.

**Global application scheduling and orchestration**

Tencent Kubernetes Engine Distributed Cloud Center provides multidimensional scheduling and orchestration capabilities to improve application services scheduling from single-cluster scheduling to multi-cluster scheduling and from node scheduling to cluster scheduling based on Tencent Cloud’s mature and reliable application scheduling and orchestration capabilities. It helps users to rationally plan resources from a global perspective, realize multi-cluster level awareness, proportional distribution, auto scaling, load balancing and other features, and complete tedious operations automatically.

**Traffic governance**

Tencent Kubernetes Engine Distributed Cloud Center works in conjunction with Services, Ingress controllers, and Service meshes of multiple clusters, providing features such as multi-cluster Service discovery, multi-cluster Ingress/Gateway, and multi-cluster NetworkPolicy to achieve traffic load balancing and service routing across multiple clusters. More over, through multi-cluster Mesh Istio, Pod-to-Pod connections across cluster boundaries are realized, and communication between services running on different clusters can be managed through Mesh.

**Application marketplace**

Users can manage multiple cloud-native products and services (Helm Chart) through cloud-native applications marketplace. Also, users can manage and distribute applications to clusters in multiple regions and owned by different cloud vendors.

**Ops center**

Tencent Kubernetes Engine Distributed Cloud Center provides complete log management, audit management, event management, health check, monitoring and alarming features based on public cloud service.

** Security and compliance**

Tencent Kubernetes Engine Distributed Cloud Center provides multiple security policies and tools, and enables users to manage security policies for multi-cloud and multi-cluster scenarios and applications in one place to meet the requirements of rules and regulations in different regions and countries.

**Automation tools**

Tencent Kubernetes Engine Distributed Cloud Center provides a variety of multi-cloud automation tools to deal with the scenarios such as multi-cloud migration of applications, cluster backup recovery, multi-site active-active disaster recovery, and multi-cloud image transfer.


## Clusternet

Tencent Cloud has provided the core features of Tencent Kubernetes Engine Distributed Cloud Center to the open-source multi-cluster application governance project [Clusternet](https://github.com/clusternet/clusternet). Any vendor and customer who is willing to build a container application platform can quickly realize multi-cluster management and application governance capabilities by integrating Clusternet.

Clusternet is designed for hybrid cloud, distributed cloud and edge computing scenarios, supports integration and management of massive clusters. Its flexible cluster registration capabilities can adapt to cluster management requirements under various complex network conditions. It is compatible with cloud-native Kubernetes APIs to reduce users’ management and Ops costs, and to accelerate the transformation of cloud-native applications.

![clusternet-arch](https://qcloudimg.tencent-cloud.cn/raw/83a1463f139a281790f65c26cbbe1f5a.png)

Clusternet provides the users with the following services:
**Managing various Kubernetes clusters in one place**
Clusternet supports managing clusters in “Pull” mode and “Push” mode. Clusternet can establish network tunnels to connect and manage the target clusters even when these clusters are running within a VPC, at the edge, or behind a firewall.

**Supports cross-cluster service discovery and service mutual access**
It provides cross-cluster access routing even in the absence of a dedicated network channel.

**Fully compatible with native Kubernetes APIs**
It is fully compatible with standard Kubernetes APIs, such as Deployment, StatefulSet and DaemonSet, as well as custom CRDs. Users only need to do simple configurations to upgrade from a single-cluster application to a multi-cluster application, without the need to learn complex multi-cluster APIs.

**Supports deployment of Helm Chart, native Kubernetes applications and custom CRDs**
It supports Helm Chart applications, including distribution, localization configuration, status aggregation of Chart. The capabilities are consistent with the native Kubernetes APIs.

**Rich and flexible configuration management**
It provides various types of configuration policies. Users can flexibly use these configurations to implement complex application scenarios, such as multi-cluster canary release.

**Simple architecture with add-ons**
It adopts the method of Aggregated ApiServer and does not rely on additional storage. The simple architecture is easy to deploy, and greatly reduces the complexity of operations.

**Easy to integrate**
Clusternet provides complete capabilities for integration, supports kubectl plugin and client-go, facilitates one-click integration of applications, and has the ability to manage multiple clusters.



## Concepts

**Container**

By containerization, all applications and their dependencies are packaged into an image, and then use the image to generate a resource-isolated environment to run the applications. This allows the applications to run independently in a consistent environment in a simple and efficient manner.

Container is a lightweight virtualization technology at the operating system level for isolating and controlling system resources, making global resources only usable in the container processes.

**Kubernetes**

Kubernetes is an open-source Container Orchestration Engine (COE) inspired by a Google project called Borg. It is one of the most important components of the Cloud Native Computing Foundation (CNCF). Kubernetes provides production-level capabilities such as application orchestration, container scheduling, service discovery, and autoscaling. For more information, see [Kubernetes Documentation](https://kubernetes.io/docs/home).


## Additional Services
Tencent Kubernetes Engine Distributed Cloud Center can provide solutions in combination with other Tencent Cloud products.
If you want to use Kubernetes container management service, it is recommended to choose [TKE](https://intl.cloud.tencent.com/zh/products/tke).
