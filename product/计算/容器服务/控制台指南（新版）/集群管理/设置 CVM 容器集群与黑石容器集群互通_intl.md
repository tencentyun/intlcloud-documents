## Operation Scenario

Peering Connection is a high-bandwidth and high-quality connectivity service that makes possible communication among Tencent Cloud resources. You can achieve inter-region cross-VPC communication among different clusters through a peering connection. This document mainly describes how to establish a peering connection between a BM VPC and a public cloud VPC to enable communication among CPM instances and containers.

>! 
> - This document uses a cluster that has been created and a node that has been added in a public cloud as an example. For more information about how to create a cluster, see [Creating a Cluster](https://cloud.tencent.com/document/product/457/11741).
> - Please make sure that the peering connection has been successfully established between BM and the public cloud and the servers can communicate with BM. If there is a problem establishing the peering connection, please check whether the **console routing table entry, security group, and subnet ACL** are correctly set. For more information about how to establish a BM VPC peering connection, see [BM VPC Peering Connection](https://cloud.tencent.com/document/product/1024/32564).

## Directions

<span id="ObtainInformation"></span>
### Getting Information

1. Log in to the [BM VPC console](https://console.cloud.tencent.com/vpcbm/vpc).
2. On the VPC management page, record the **CIDR** of the created BM VPC. See the figure below:
![](https://upload-images.jianshu.io/upload_images/13878457-9d7ab72b55bab74e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. Switch to the [TKE console](https://console.cloud.tencent.com/tke2).
4. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster)** to go to the cluster management page.
5. Click the ID/name of the cluster where communication needs to be set to enter the cluster management page. See the figure below:
![](https://main.qcloudimg.com/raw/d87f3d03f6c97313927eb93ddc885518.png)
6. In the left sidebar, select "Basic information" to go to the "Basic information" page. See the figure below:
![](https://main.qcloudimg.com/raw/ff32de50dadbee103621862412ae08cc.png)
7. Record the information of "Region", "Node network", and "Container network" in "Basic information".
8. Click **Account** > **[Account information](https://console.cloud.tencent.com/developer)** at the top right to record the APPID of the current account. See the figure below:
![](https://main.qcloudimg.com/raw/a9057017451dbe67837a0867cf6022ab.png)
9. Switch to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
10. In the left sidebar, click **[Peering Connection](https://console.cloud.tencent.com/vpc/conn)** to go to the peering connection management page and record the ID/name of the peering connection. See the figure below:
![](https://main.qcloudimg.com/raw/cdd10b18030ba60e2d73414dfbc24118.png)

### Applying for a Peering Connection

[Submit a ticket](https://console.cloud.tencent.com/workorder) and enter the "Region", "Node network", "Container network", and APPID of the current account recorded in the [Getting Information](#ObtainInformation) section in the ticket.

### Expected Result

Containers can communicate with CPM instances. For the login method of the public cloud cluster container, see [Basic Operations of a Remote Terminal](https://cloud.tencent.com/document/product/457/9120).
1. Log in to the public cloud cluster container and access the CPM instance from there. See the figure below:
![Container accesses CPM instance](https://main.qcloudimg.com/raw/473e522adffdd20550762c597b61f0ba.png)
2. Log in to the CPM instance and access the public cloud cluster container from there. See the figure below:
![CPM instance accesses container](https://upload-images.jianshu.io/upload_images/13878457-3c050d5c47b569ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
