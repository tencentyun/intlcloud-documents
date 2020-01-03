## Operation Scenario

Peering Connection is a high-bandwidth and high-quality connectivity service that makes possible communication among Tencent Cloud resources. You can achieve inter-region cross-VPC communication among different clusters through a peering connection. 

>- This document uses a cluster that has been created and a node that has been added as an example. For more information about how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
> - Please make sure that the peering connection has been successfully established and the servers can communicate with one another. If there is a problem establishing the peering connection, please check whether the **console routing table entry, CVM security group, and subnet ACL** are correctly set.
> - Currently, communication is only supported for clusters over an **inter-region peering connection**. If you need cross-region communication among containers, please submit a ticket.

## Directions


### Getting Basic Information of a Container

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. <span id="step3">Click the ID/name of the cluster where inter-region cross-cluster communication needs to be set to enter the cluster management page. See the figure below: </span>
For example, go to the management page of cluster A.
![](https://main.qcloudimg.com/raw/37757652cd5c8fe05452c961ce35020a.png)
4. In the left sidebar, select "Basic information" to go to the "Basic information" page. See the figure below:
![](https://main.qcloudimg.com/raw/7e0db2c6133f1c6b0af40dfc833147d3.png)
5. <span id="step5">Record the IP address range and mask of the "Container network" in "Basic information". </span>
6. Repeat [step 3](#step3) to [step 5](#step5) and record the IP address range and mask of the container network of another cluster.
For example, you can record the IP address range and mask of the container network of cluster B.

### Configuring a Routing Table

1. Switch to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. <span id="VPCStep2">In the left sidebar, click **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** to go to the subnet management page. </span>
3. Click the local end of the peering connection and specify the routing table associated with the subnet. See the figure below:
![](https://main.qcloudimg.com/raw/fd61cd59e135f9f7de1b528a17a80779.png)
4. On the "Default details" page of the associated routing table, click **+ Create a routing policy**.
5. In the "Create a route" window that pops-up, set the routing information. Main parameters include:
 - Destination: Enter the IP address range of cluster B container.
 - Next hop type: Select "**Peering connection**".
 - Next hop: Select the established peering connection.
6. <span id="VPCStep6">Click **OK** to complete the configuration of the routing table of the local end. </span>
7. Repeat [step 2](#VPCStep2) to [step 6](#VPCStep6) to complete the configuration of the routing table of the opposite end.

### Expected Result

Containers can communicate with one another. For the login method of the container, see [Basic Operations of a Remote Terminal](https://intl.cloud.tencent.com/document/product/457/9120).
1. Log in to the container of cluster A and access the container of cluster B from there. See the figure below:
![](https://main.qcloudimg.com/raw/61f44f2ffc028a4000282a6e1ca24fb0.png)
2. Log in to the container of cluster B and access the container of cluster A from there. See the figure below:
![](https://main.qcloudimg.com/raw/5c7302cec8b1199bf2ef6cded48c2a95.png)

