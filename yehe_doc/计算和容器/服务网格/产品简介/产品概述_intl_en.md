
## Overview
Tencent Cloud Mesh is a consistent, reliable, and transparent communication network management and control platform for cloud-native applications. It is fully compatible with Istio APIs. It is natively integrated with the Tencent Cloud infrastructure, and provides fully-managed service-oriented support capabilities, thereby easily guaranteeing and managing mesh lifecycles.
Being seamlessly connected to IaaS networking and integrated with monitoring components, Tencent Cloud Mesh is out of the box, which reduces operations costs. It flexibly accesses and manages applications across clusters, environments, and architectures to obtain consistent discovery, traffic, observation, and security management and control capabilities, thereby accelerating cloud-native transformation and migration of services. It has extended and enhanced high-level features such as data plane operations, ingress gateway, and configuration telemetry. In addition, it has been deeply optimized to provide better data plane forwarding performance, and comprehensively cover north-south and east-west communication connections of applications.

![](https://qcloudimg.tencent-cloud.cn/raw/b160a55a41313b2c61376d0cfcad63c4.png)



## Core Concepts

#### Service mesh

A service mesh is logical isolation space that manages and controls communication networks between services, and provides a consistent and transparent service discovery, traffic, and full-link observation management environment. A same mesh can manage services from multiple Kubernetes clusters and even heterogeneous VMs. Services in the same mesh can communicate with each other by default.

#### Service

A service is a basic unit for a service mesh to manage traffic. One service can correspond to multiple endpoint instances. The corresponding relationship can come from automatic discovery of the service mesh on K8s services of Kubernetes clusters, or the corresponding relationship between endpoint instances and services can be manually registered.

#### Data plane

A data plane includes a gateway and a sidecar proxy. The gateway is deployed as an independent pod in a Kubernetes service discovery cluster of a mesh to control and observe north-south traffic. The sidecar proxy is deployed in a service pod or a service virtual machine to control and observe east-west traffic.

#### Control plane

A control plane manages and configures the data plane to route and forward traffic.

#### Istio CRD

A custom resource definition (CRD) is an extension of a default Kubernetes API. Tencent Cloud Mesh is compatible with Istio's Kubernetes CRD APIs and uses them to configure east-west and north-south service traffic control policies in a mesh.

## Features

![](https://qcloudimg.tencent-cloud.cn/raw/786e6a55e7e774e747085c78244e0614.png)

## Pricing

Tencent Cloud Mesh is billed based on two dimensions, that is, the number of clusters and the number of online sidecars. For details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1152/47435).

## Additional Services

- [Tencent Kubernetes Engine (TKE)](https://intl.cloud.tencent.com/document/product/457): Services managed by a service mesh come from TKE clusters through automatic service discovery.
- [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003): When services managed by a service mesh come from different VPCs or regions, CCN is required to connect cross-VPC networks.
- [Cloud Load Balancer (CLB)](https://intl.cloud.tencent.com/document/product/214): An ingress gateway of a service mesh is integrated with CLB to realize fine-grained traffic management at the access layer of the service mesh.
- [Managed Service for Prometheus (TMP)](https://intl.cloud.tencent.com/document/product/457/44033): Tencent Cloud Mesh supports connecting monitoring metrics to Prometheus instances managed by TMP, which automatically configures and collects mesh monitoring data and is preset with a Tencent Cloud Mesh Grafana dashboard.
- [Cloud Log Service (CLS)](https://intl.cloud.tencent.com/document/product/614): Tencent Cloud Mesh supports collecting access logs to CLS. The logs can be viewed and retrieved on the CLS console.
