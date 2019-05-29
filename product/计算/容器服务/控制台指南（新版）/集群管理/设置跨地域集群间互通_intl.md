## Operation Scenario


Peering Connection is a high-bandwidth and high-quality connectivity service that makes possible communication among Tencent Cloud resources. For more information about how to establish a peering connection, see [Creating a Peering Connection](https://cloud.tencent.com/document/product/553/18836). You can achieve cross-region communication among different clusters through a peering connection.
>! 
> - This document uses a cluster that has been created and a node that has been added as an example. For more information about how to create a cluster, see [Creating a Cluster](https://cloud.tencent.com/document/product/457/11741).
> - Please make sure that the peering connection has been successfully established and the servers can communicate with one another. If there is a problem establishing the peering connection, please check whether the **console routing table entry, CVM security group, and subnet ACL** are correctly set.

## Directions

### Getting Basic Information of a Container

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. <span id="step3">Click the ID/name of the cluster where cross-region cross-cluster communication needs to be set to enter the cluster management page. See the figure below: </span>
For example, go to the management page of cluster A.
![](https://main.qcloudimg.com/raw/d87f3d03f6c97313927eb93ddc885518.png)
4. In the left sidebar, select "Basic information" to go to the "Basic information" page. See the figure below:
![](https://main.qcloudimg.com/raw/ff32de50dadbee103621862412ae08cc.png)
5. <span id="step5">Record the information of "Region", "Node network", and "Container network" in "Basic information". </span>
6. Repeat [step 3](#step3) to [step 5](#step5) and record the information of "Region", "Node network", and "Container network" of another cluster container.
For example, you can record the information of "Region", "Node network", and "Container network" of cluster container B.

### Configuring a Routing Table

1. Switch to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. In the left sidebar, click **[Peering Connection](https://console.cloud.tencent.com/vpc/conn)** to go to the peering connection management page and record the **ID/name** of the peering connection. See the figure below:
![](https://main.qcloudimg.com/raw/a4c3a0168f3a0ac7feb4051a1cac78d5.png)
3. <span id="VPCStep3">In the left sidebar, click **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** to go to the subnet management page. </span>
4. Click the local end of the peering connection and specify the routing table associated with the subnet. See the figure below:
![](https://main.qcloudimg.com/raw/472c8ef4d50f463d84652ebabb42e4c4.png)
5. On the "Default details" page of the associated routing table, click **+ Create a routing policy**.
6. In the "Create a route" window that pops-up, set the routing information. Main parameters include:
 - Destination: Enter the IP address range of cluster B container.
 - Next hop type: Select "**Peering connection**".
 - Next hop: Select the established peering connection.
7. <span id="VPCStep7">Click **OK** to complete the configuration of the routing table of the local end. </span>
8. Repeat [step 3](#VPCStep3) to [step 7](#VPCStep7) to complete the configuration of the routing table of the opposite end.

### Expected Result

Containers can communicate with one another. For the login method of the container, see [Basic Operations of a Remote Terminal](https://cloud.tencent.com/document/product/457/9120).
1. Log in to the container of cluster A and access the container of cluster B from there. See the figure below:
![A Pod in Shanghai accesses a Pod in Beijing](http://upload-images.jianshu.io/upload_images/13878457-2be2ee954cabf0a4?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2. Log in to the container of cluster B and access the container of cluster A from there. See the figure below:
![A Pod in Beijing accesses a Pod in Shanghai](http://upload-images.jianshu.io/upload_images/13878457-f849ccbd9ed89294?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
