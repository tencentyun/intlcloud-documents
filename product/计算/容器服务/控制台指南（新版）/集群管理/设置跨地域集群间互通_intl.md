## Operation Scenario


Peering Connection is a high-bandwidth and high-quality connection service that links Tencent Cloud resources.You can achieve cross-region communication among different clusters through a peering connection.
>- This document uses a cluster that has been created and a node that has been added as an example. For more information about how to create a cluster, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/30637).
> - Please make sure that the peering connection has been successfully established and the servers can communicate with one another. If there is a problem establishing the peering connection, please check whether the **console routing table entry, CVM security group, and subnet ACL** are correctly set.

## Directions

### Getting Basic Information of a Container

1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. In the left sidebar, click **[Clusters](https://console.cloud.tencent.com/tke2/cluster?rid=1)** to go to the cluster management page.
3. <span id="step3">Click the ID/name of the cluster where cross-region cross-cluster communication needs to be set to enter the cluster management page. See the figure below: </span>
For example, go to the management page of cluster A.
![](https://main.qcloudimg.com/raw/505810aef1fd615d1c577b1c8bc2ba98.png)
4. In the left sidebar, select "Basic information" to go to the "Basic information" page. See the figure below:
![](https://main.qcloudimg.com/raw/1b75478c7d2f52b27b2f30067f9fbfd3.png)
5. <span id="step5">Record the information of "Region", "Node network", and "Container network" in "Basic information". </span>
6. Repeat [step 3](#step3) to [step 5](#step5) and record the information of "Region", "Node network", and "Container network" of another cluster container.
For example, you can record the information of "Region", "Node network", and "Container network" of cluster container B.

### Configuring a Routing Table

1. Switch to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. In the left sidebar, click **[Peering Connection](https://console.cloud.tencent.com/vpc/conn)** to go to the peering connection management page and record the **ID/name** of the peering connection. See the figure below:
![](https://main.qcloudimg.com/raw/8d6a540d2f80725f26ce3b70c04a5b86.png)
3. <span id="VPCStep3">In the left sidebar, click **[Subnet](https://console.cloud.tencent.com/vpc/subnet)** to go to the subnet management page. </span>
4. Click the local end of the peering connection and specify the routing table associated with the subnet. See the figure below:
![](https://main.qcloudimg.com/raw/36a03b27d4f5fcf935f01038495bb3fa.png)
5. On the "Default details" page of the associated routing table, click **+ Create a routing policy**.
6. In the "Create a route" window that pops-up, set the routing information. Main parameters include:
 - Destination: Enter the IP address range of cluster B container.
 - Next hop type: Select "**Peering connection**".
 - Next hop: Select the established peering connection.
7. <span id="VPCStep7">Click **OK** to complete the configuration of the routing table of the local end. </span>
8. Repeat [step 3](#VPCStep3) to [step 7](#VPCStep7) to complete the configuration of the routing table of the opposite end.

### Expected Result

Containers can communicate with one another. For the login method of the container, see [Basic Operations of a Remote Terminal](https://intl.cloud.tencent.com/document/product/457/9120).
1. Log in to the container of cluster A and access the container of cluster B from there. See the figure below:
![A Pod in Shanghai accesses a Pod in Beijing](https://main.qcloudimg.com/raw/eee15a6e0305127e2f56ae6ed2abe8b2.png)
2. Log in to the container of cluster B and access the container of cluster A from there. See the figure below:
![A Pod in Beijing accesses a Pod in Shanghai](https://main.qcloudimg.com/raw/70b28f7203c4b8dffed21716abdbf877.png)
