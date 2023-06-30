Service discovery is to add specific services to a mesh. It is a prerequisite for service governance and observation. Tencent Cloud Mesh supports automatic discovery of services in K8s clusters. You only need to add clusters to the mesh, including TKE and EKS clusters provided by Tencent Cloud, and third-party K8s clusters registered with TKE.


For other services other than K8s, such as VM, cloud database, you can manually register them with the mesh by configuring ServiceEntry, WorkloadGroup, and WorkloadEntry.
![](https://main.qcloudimg.com/raw/f4691a40bb91d3fc2d8ebc484d56e48d.png)

For details about how to add K8s clusters and heterogeneous services to Tencent Cloud Mesh, see the following sections:

- [Automatic Service Discovery](https://intl.cloud.tencent.com/document/product/1152/47468)
- [Manual Service Discovery](https://intl.cloud.tencent.com/document/product/1152/47469)



