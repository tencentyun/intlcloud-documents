## Operation Scenarios
This document describes how a workload provides an open API through Service and Ingress.


## Prerequisites
- An elastic cluster has been created and is in the Running state. For more information, see [Creating a Cluster](https://cloud.tencent.com/document/product/457/39813).
- The cluster has an appropriate namespace that is in the Active state.

## Introduction to Service Types
### Service
A Service defines a policy for gaining access to backend pods and provides a static virtual IP address for access. You can gain access to backend pods in load balancing mode through Service.

A Service supports the following access modes:
- Internet-based access: you can use the Loadbalance mode of Service to enable access to backend pods through a public IP address. In this mode, a public CLB is automatically created.
- Intra-cluster access: you can use the ClusterIP mode of Service to enable access to backend pods from within a cluster. Elastic clusters only support Headless ClusterIP Services.
- VPC-based access: you can use the Loadbalance mode of Service to enable access to backend pods from a VPC through a private IP address by specifying `annotations:service.kubernetes.io/qcloud-loadbalancer-internal-subnetid: subnet-xxxxxxxx`. In this mode, a private CLB is automatically created.


### Ingress
An Ingress is a collection of rules that enables access to Services within a cluster. You can configure different forwarding rules to allow access from different URLs to different Services within a cluster.

To ensure the proper running of Ingress resources, you must run an Ingress controller in a cluster. TKE enables the CLB-based `l7-lb-controller` in a cluster by default and supports HTTP, HTTPS, and NGINX Ingress controllers. You can select different types of Ingress controllers based on your business needs.


## Procedure
For the specific procedure, see [Service Management](https://intl.cloud.tencent.com/document/product/457/30672) and [Ingress Management](https://intl.cloud.tencent.com/document/product/457/30673).

## Notes
- In an elastic cluster, only Headless ClusterIP Services can be created for intra-cluster access.
- In an elastic cluster, a CLB created through a Service is directly bound to the ENIs of all the pods within the endpoint.
- In an elastic cluster, Services only support [CLBs](https://intl.cloud.tencent.com/document/product/214/8847).
- To create a Service by using an existing CLB, you must ensure that the CLB is not bound to any listener.
