Accessing an ingress gateway from the public network fails.

## Common Cause

### Security Group Does Not Allow NodePort

By default, an ingress gateway installed on Tencent Cloud Mesh is exposed by binding CLB to NodePort. Therefore, the traffic link is: client –> CLB –> NodePort –> ingress gateway.

The key link is CLB –> NodePort. SNAT is not performed on a data packet forwarded by CLB. Therefore, when the packet arrives at a node, the source IP address is the public IP address of the client. If an inbound rule of a security group of the node does not allow the link client –> NodePort, the ingress gateway is inaccessible.

**Solution 1:** Set a NodePort range (30000-32768) for public access in the inbound rule of the security group of the node. 

![](https://qcloudimg.tencent-cloud.cn/raw/8e7979e8f81dd8737778ffddd0464841.png)

**Solution 2:** If you are concerned about the security risk of directly allowing all ports in the entire NodePort range, you can expose only the NodePorts used by the ingress gateway service.

**Solution 3:** If only clients in a fixed IP segment are allowed to access the ingress gateway, all ports in the entire NodePort range can be opened only to this IP segment.

**Solution 4:** Enable CLB-to-pod direct access for the ingress gateway. In this way, traffic does not pass through the NodePort, and no security group issue occurs. Before enabling CLB-to-pod direct access, ensure that the cluster network supports VPC-CNI. For details, see [How to Enable CLB-to-Pod Direct Access](https://imroc.cc/k8s/tke/faq/loadblancer-to-pod-directly/).

