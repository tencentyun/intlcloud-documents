## Scenario
This document describes how to expose workloads for access through Services.

## Prerequisites
- You have an edge cluster that is in the Running state. For more information, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
- The cluster has an appropriate namespace that is in the Active state.

## Service Types
### Service
A Service defines a policy for gaining access to backend pods and provides a static virtual IP address for access. You can gain access to backend pods in load balancing mode through the Service.

Services support the following types:
- ClusterIP: provides an entry that is reachable by other Services or containers within the cluster. This type supports the TCP/UDP protocol. For example, it can be utilized by MySQL services to ensure network isolation. For more information, see [Kubernetes Service](https://kubernetes.io/docs/concepts/services-networking/service/).
- NodePort: provides an access method by mapping a node port to a container. This type supports the TCP/UDP protocol. It is useful when you want to load-balance your businesses to nodes. For more information, see [Kubernetes Service](https://kubernetes.io/docs/concepts/services-networking/service/).


## Directions
For Service-related operations, see [Service Management](https://intl.cloud.tencent.com/document/product/457/30672).
>!Intra-cluster access of edge clusters only supports Kubernetes native access methods. To use VPC instances on the computing resource side, you need to integrate the VPC solutions of your cloud providers.
