## Cloud Connect Network
[Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003/30049) interconnects Virtual Private Clouds (VPCs) or VPCs and local IDCs. You can add VPCs and direct connect gateway instances to the CCN to enjoy single-point access and network-wide resource sharing. This way, you can build a simple, intelligent, secure, and flexible hybrid cloud and a globally interconnected network.


## Introduction
You can register existing container clusters to the CCN, and the CCN will manage the container network. After the container network is registered, you can enable or disable routes of the container network IP range on the CCN side to ensure interconnection between the container clusters and resources in CCN.
> After a container cluster is registered to the CCN, its IP range will be enabled when it does not conflict with existing routes in the CCN instance, and it will be disabled by default when there are conflicts.





## Prerequisites
- The VPC of the cluster is already in the CCN. For more information about operations related to CCN, please see [CCN Operations Overview](https://intl.cloud.tencent.com/document/product/1003/30061).
- The IP range of the cluster's container network does not conflict with the IP ranges of other resources in the CCN.


## Directions

### Registering a container network to the CCN
1. Log in to the TKE console and click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** in the left sidebar to go to the cluster management page.
2. Click the ID of the cluster that you want to register to the CCN, and click **Basic Info** on the left to go to the cluster basic information page.
3. Click the CCN registration button to register the container network to the CCN, as shown below:
> This step only registers the container’s IP range to the CCN. Whether the route takes effect depends on your configuration on the CCN side.

![](https://main.qcloudimg.com/raw/ff0a346802069809892bf0241d64687d.png)




### Viewing routes of the container IP range
1. Log in to the VPC console and click **[CCN](https://console.qcloud.com/vpc/ccn)** in the left sidebar to go to the CCN management page.
2. Click **Manage Instance** next to the CCN associated with the cluster VPC to go to the CCN instance management page, as shown below:
![](https://main.qcloudimg.com/raw/49143db7cbcabe993574eb670256cab0.png)
3. Click the **Route Table** tab to check whether the route of the container network IP range is enabled, as shown below:
>
>- If the IP range of the container network does not conflict with existing routes in the CCN instance, the route will be enabled by default. If there is an IP range conflict, the route will be disabled by default.
>- For more information about route conflicts, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052). If you want to enable a route that may lead to conflicts, see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

![](https://main.qcloudimg.com/raw/d28a8232ed5b4e33aa51768d08d604d3.png)
4. Test the interconnection between the container cluster and other resources in the CCN.








