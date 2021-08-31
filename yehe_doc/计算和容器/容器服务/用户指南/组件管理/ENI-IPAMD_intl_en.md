

## Add-on description

ENI-IPAMD is a GRPC server that runs on specific nodes or the master. It can help manage IP resource allocation, reserve IP addresses for the StatefulSet controller, and allocate and manage the host secondary ENI for node controller.

**When VPC-CNI network mode is selected in cluster, ENI-IPAMD will be installed automatically.** 
- VPC-CNI is an extended network mode supported by TKE. In VPC-CNI mode, Tencent Cloud ENI assigns IP addresses within the VPC instance to pods in the cluster, and the Tencent Cloud VPC instance is responsible for routing. In this way, the data plane and control plane of pods and nodes can be located at the same network layer. VPC-CNI pods can use all product features of Tencent Cloud VPC.
- In VPC-CNI mode, StatefulSet supports pods with static IP addresses. The IP addresses of these pods do not change after the pods are restarted or migrated. Therefore, they are suitable for scenarios that require to restrict accesses or query logs based on source IPs.
>! The VPC-CNI mode has use limits. We recommend that you check whether the mode adapts to your business scenarios in advance.



## Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Default Resource Occupation | Namespaces |
| ------------------- | ---------- | ------------------------ | --------------- |
| tke-eni-ipamd | Deployment | CPU: 100m<br>memory: 100Mi | kube-system |
| tke-eni-agent | DaemonSet | CPU: 10m | kube-system |
| tke-eni-ipamd       | Service    | -                        | kube-system     |
| tke-cni-agent-conf  | ConfigMap  | -                        | kube-system     |

## References
- [VPC-CNI Network Mode User Guide](https://intl.cloud.tencent.com/document/product/457/38712)
- [GlobalRouter VPC-CNI Mode Description](https://intl.cloud.tencent.com/document/product/457/35250)
