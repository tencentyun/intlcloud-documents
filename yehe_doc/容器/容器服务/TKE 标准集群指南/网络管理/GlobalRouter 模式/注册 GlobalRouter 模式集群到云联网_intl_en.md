## Cloud Connect Network
[Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003/30049) provides interconnection among Virtual Private Clouds (VPCs) and between VPCs and local IDCs. You can add VPCs and Direct Connect gateway instances to the CCN to achieve single-point access and network-wide resource sharing for a simple, intelligent, secure, and flexible hybrid cloud and globally interconnected network.


## Overview
You can register existing container clusters to CCN, and CCN will include the containers’ network in its scope of management. After the containers’ network is fully registered, you can enable or disable the IP range routing of the containers’ network on the CCN side to achieve interconnection between the container clusters and resources in CCN.
>! After a container cluster is registered to CCN, its IP range will be enabled when it does not conflict with the existing routing in the CCN instance, and it will be disabled by default when there are conflicts.





## Prerequisites
- The VPC of the cluster is already in CCN. For operations related to CCN, see [CCN Operations Overview](https://intl.cloud.tencent.com/document/product/1003/30061).
- You have evaluated whether the IP range of the cluster’s network conflicts with the IP ranges of other resources in CCN.


## Directions

### Registering Container Network to CCN
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar to go to the cluster management page.
2. Click the ID of the cluster you want to register to CCN, and click **Basic Info** on the left to go to the cluster basic information page.
3. Toggle on the CCN registration button to register the container network to the CCN as shown below:
>! This step only registers the container IP range to the CCN. Whether or not the routing takes effect depends on your configuration on the CCN side.
>
![](https://main.qcloudimg.com/raw/0615d4b5ac0c3dd42e8ff28b2b350c41.png)




### Viewing the IP Range Routing of the Container
1. Log in to the VPC console and click **[CCN](https://console.qcloud.com/vpc/ccn)** in the left sidebar to go to the CCN management page.
2. Click **Manage Instance** to the right of the CCN associated with the cluster VPC to go to the CCN instance management page as shown below:
![](https://main.qcloudimg.com/raw/1612987cc3aa60ea57ac284b7b61ccfa.png)
3. Click the **Route Table** tab to view whether the container’s IP range routing is enabled or not as shown below:
>?
>- If the IP range of the cluster network does not conflict with the existing routing in the CCN instance, the routing will be enabled by default. If there is an IP range conflict, the routing will be disabled by default.
>- For more information on routing conflicts, see [Use Limit > Route Restrictions](https://intl.cloud.tencent.com/document/product/1003/30052). If you want to enable a route that may lead to routing conflicts, read [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).
>
![](https://main.qcloudimg.com/raw/0d7beab6c11c1c22f2ebcd20fc93f7f9.png)
4. Test the interconnection between the container cluster and other resources in the CCN.














