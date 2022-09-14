## Introduction
This document describes how to use Service and Ingress as entry points to expose workloads to external sources.

## Service Types
### Service
Service defines policies for accessing backend Pods and provides a fixed virtual IP address for access. It also provides load balancing for all requests to Pods.

Service can be of the following types:
- Public network access: the public network access Service uses operates in Loadbalance and automatically creates a public network CLB instance. Public IP addresses can access backend Pods.
- Intra-cluster access: the intra-cluster access Service operates in ClusterIP mode and is used for access within the cluster.
- VPC private network access: the VPC private network access Service operates in Loadbalance and automatically creates a private network CLB instance. By using `annotations:service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx`, you can use a private IP address from the VPC private network to access the backend Pod.

>! When the service type is public network access, `ClusterIP` of this service is disabled by default. You can add the following annotations in yaml to enable `ClusterIP`:
```java
service.kubernetes.io/qcloud-clusterip-loadbalancer-subnetid: #Subnet ID of the service CIDR
```

### Ingress
Ingress is a collection of rules that allow access to Services of a cluster. You can configure different forwarding rules to allow different URLs to access different Services.

In order for Ingress resources to operate properly, you must run `Ingress-controller`. TKE enables the CLB-based `l7-lb-controller` by default and supports HTTP, HTTPS, and nginx-ingress controllers. You can select Ingress controllers according to your needs.

## Prerequisites
- You have created an elastic cluster that is in the Running state. For more information, see [Creating a cluster](https://intl.cloud.tencent.com/document/product/457/34048).
- The cluster has an appropriate namespace that is in the Active state.

## Directions
For more information and instructions, see [Service Management](https://intl.cloud.tencent.com/document/product/457/30672) and [Ingress Management](https://intl.cloud.tencent.com/document/product/457/37013).

## Considerations
- Creating ClusterIP Service in an serverless cluster uses IP addresses from the Service CIDR. Make sure there are enough IP addresses in the subnet.
In an serverless cluster, a CLB instance created by the Service binds all ENIs of all Pods within the endpoint.
- In an serverless cluster, Services only supports [CLB](https://intl.cloud.tencent.com/document/product/214/8847) instances.
- To create a Service using an existing CLB, you must ensure that the CLB is not bound to any listener.
