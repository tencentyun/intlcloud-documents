## Overview
A Tencent Cloud Mesh can associate with multiple TKE clusters and automatically discover K8s services in the clusters. You can associate multiple TKE clusters when creating the mesh or on the mesh basic information page, and Tencent Cloud Mesh will automatically display the services in the clusters on the **Service** page.

## Limits

- **Cluster quota**: A single mesh supports up to 10 K8s clusters by default, and the clusters in the mesh are deployed across up to three regions. After the quota is exceeded, you cannot add more clusters to the mesh.
- **Cluster version**: Tencent Cloud Mesh does not enforce that the cluster versions are exactly the same, but the cluster versions should meet requirements of Istio for the corresponding K8s versions. For details, see [Supported Releases](https://istio.io/latest/docs/releases/supported-releases/).
- **Cluster permission**: You need to have admin permissions for the cluster to be added to the mesh. For details, see [Adding Mesh Permissions for a Cluster](https://intl.cloud.tencent.com/document/product/1152/47498).
- **VPC network**: To ensure the normal access to pods across multiple clusters that are not in the same VPC, use [CCN](https://intl.cloud.tencent.com/document/product/1003) to connect these clusters. Add the clusters to the same CCN instance. **Ensure that the host CIDR and container CIDR in the VPC at each end of the CCN instance do not conflict.**
- **Container network**: If a TKE cluster uses the Global Router mode, you need to [register the container network with CCN](https://intl.cloud.tencent.com/document/product/457/43391), so that newly added container CIDRs can be accessed.

## Directions

### Mesh creation page

You can add an automatic service discovery cluster when creating a mesh on the mesh creation page.

1. Log in to the [Tencent Cloud Mesh console](https://console.cloud.tencent.com/tke2/mesh).
2. Click **Create** to create a service mesh.
3. Click **Add cluster** next to **Service discovery** under **Basic information**.
![](https://qcloudimg.tencent-cloud.cn/raw/0745016518ee57b5ea8dbd57b8785707.png)
4. Select one or more Kubernetes automatic service discovery clusters to be added. After the mesh creation request is submitted, the created mesh instance can automatically discover K8s services in the cluster.
![](https://qcloudimg.tencent-cloud.cn/raw/a33986c5e45e4ec30ee9c190a150389e.png)

### Mesh details page

On the mesh details page, you can view the service discovery clusters associated with the current mesh instance, and add or disassociate an automatic service discovery cluster.

#### Adding a service discovery cluster 

1. Go to the mesh details page, and click **Basic information** in the sidebar. In the **Service discovery** module, you can view the list of service discovery clusters associated with the mesh. Then, click **Add** to pop up the **Add service discovery cluster** window.
![](https://qcloudimg.tencent-cloud.cn/raw/e013c234609672a45dd0092ec30110c0.png)
2. In the **Add service discovery cluster** window, select one or more Kubernetes service discovery clusters to be added, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/2e823aa6a27980ff379f80f2ef1e4938.png)
3. After the request for adding a Kubernetes service discovery cluster is submitted, wait for the cluster to be connected. After the cluster is connected, addition of the Kubernetes service discovery cluster is complete.
![](https://qcloudimg.tencent-cloud.cn/raw/0038fb53797ac76cedc77a3f361193d1.png)

>! After the service is added to the mesh, you need to inject a sidecar into the service and then perform management operations on the service, such as traffic management and visual observation. For related guidelines, see [Mesh Configuration](https://intl.cloud.tencent.com/document/product/1152/47464).

#### Disassociating a service discovery cluster

You need to disassociate a service discovery cluster that does not need to participate in mesh management or a deleted cluster to avoid unnecessary fees. You can follow the following steps:

> * For a deleted cluster, Tencent Cloud Mesh will not automatically disassociate it for you, but will not charge cluster management fees any longer.
> * If the only cluster in the mesh is deleted, Tencent Cloud will force you to disassociate it to ensure normal mesh experience.

1. Go to the mesh details page, and click **Basic information** in the sidebar. In the **Service discovery** module, you can view the list of service discovery clusters associated with the mesh. Then, in the **Operation** column where the cluster to be disassociated resides, click **Disassociate** to pop up a dialog box for confirming disassociation.
![](https://qcloudimg.tencent-cloud.cn/raw/fe93df9f6243c49f569e69af3e74d596.png)
2. In the **Disassociation** dialog box, confirm the information about the service discovery cluster to be deleted, and click **OK** to submit the cluster disassociation request. After the cluster is disassociated, the mesh is no longer aware of service instance changes in the cluster and related service requests may become abnormal.
![](https://qcloudimg.tencent-cloud.cn/raw/f83a46ebd775d3003e788e3db0646fa3.png)
3. Wait for the disassociation operation to complete.
![](https://qcloudimg.tencent-cloud.cn/raw/d5134f39d5e9bcf4e6b2149b1caffeee.png)
