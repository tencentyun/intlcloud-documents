### How do I establish or delete a peering connection?
See [Workflow for Establishing or Deleting Peering Connections](https://cloud.tencent.com/document/product/553/18840#.E5.BB.BA.E7.AB.8B.E5.AF.B9.E7.AD.89.E8.BF.9E.E6.8E.A5.E6.B5.81.E7.A8.8B) for how to establish or delete a peering connection.

### How do I configure route tables for both ends of a peering connection?
Use the following steps to configure route tables for both ends of a peering connection:
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), click **Products** -> **Cloud Compute & Network** -> **Virtual Private Cloud**, and then click **Subnets** in the left pane on the console.
2. Click the ID of the route table with which the specified requester subnet of the peering connection is associated (e.g. gateway) to go to the details page.
![](https://main.qcloudimg.com/raw/f362db96231b3b1cefc182cd098ec1c4.png)
3. Click **+ New routing policies**
![](https://main.qcloudimg.com/raw/3cbcb6bce2afe5adf33884a5457a9eef.png)
4. In the **Add routing** window, enter the accepter CIDR (10.0.1.0/24) for the destination, select **Peering Connections** for next hop type, and select the created peering connection (PeerConn) for the next hop. Click **OK** to save the route table.
![](https://main.qcloudimg.com/raw/7ba0600382eafe22f1f6525a0714868b.png)

Follow the same process as above to configure the accepter route table.

>**Notes:**
>- You must configure routes on both ends before you can communicate via the peering connection.
>- For communication between multiple IP address ranges of two VPCs on both ends, you only need to increase the corresponding route table entries instead of creating multiple peering connections. After the route table is configured, the communication can be achieved between different IP address ranges of two VPCs.

### How do I view relevant routing policies?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to view peering connection related routing policies. For more information, see [View Relevant Routing Policies](https://cloud.tencent.com/document/product/553/18841).

### How do I view monitoring data of network traffic over cross-region peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to view monitoring data of network traffic over a cross-region peering connection. For more information, see [View Monitoring Data of Network Traffic over Cross-region Peering Connections](https://cloud.tencent.com/document/product/553/18842).

### How do I configure traffic control for cross-region peering connections?
- Network traffic over intra-region peering connection is free of charge. No traffic control is applicable. The bandwidth cap is 5 Gbps.
- Traffic control is supported for cross-region peering connection.

You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to configure traffic control for a cross-region peering connection. For more information, see [Configure Traffic Control for Cross-region Peering Connections](https://cloud.tencent.com/document/product/553/18843).

### How do I enable traffic control details for peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to enable traffic control details for a peering connection. For more information, see [Enable Traffic Control Details for Peering Connections](https://cloud.tencent.com/document/product/553/18844).

### How do I set traffic control details for peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to set traffic control details for a peering connection. For more information, see [Set Traffic Control Details for Peering Connections](https://cloud.tencent.com/document/product/553/18845).

### How do I view traffic control details for peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to view traffic control details for a peering connection. For more information, see [View Traffic Control Details for Peering Connections](https://cloud.tencent.com/document/product/553/18846).

### How do I view the accepter account ID?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to view the accepter account ID. For more information, see [View Accepter Account IDs](https://cloud.tencent.com/document/product/553/18849).

### How do I reject peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to reject a peering connection. For more information, see [Reject Peering Connections](https://cloud.tencent.com/document/product/553/18847).

### How do I activate cross-region connectivity of basic networks?
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=168&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC) for activating cross-region connectivity of basic networks.

### How do I set alarms for cross-region connectivity?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to set alarms for cross-region connectivity. For more information, see [Set Alarms for Cross-region Connectivity](/document/product/553/18851).
### How do I delete peering connections?
You can go to [Tencent Cloud Console](https://console.cloud.tencent.com/) to delete a peering connection. For more information, see [Delete Peering Connections](/document/product/553/18848).

### How do I implement cross-region connectivity?
Implement cross-region connectivity by completing the following steps:
1. Create a peering connection.
2. Set route tables on both ends.

For more information, see [Implement Communication over Peering Connections under the Same Account](/document/product/553/18836).













