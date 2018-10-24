1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> **Virtual Private Cloud** to go to the VPC console.
2. In the left pane, click **Subnets** to go to the management page.
3. Click the ID of the route table (route table A) associated with the specified subnet (subnet A) on requester end of the peering connection, to enter the details page of the route table.
 ![](https://main.qcloudimg.com/raw/0ea8477fe4e80d805dab74c74415146a.png)
4. Click **+ New routing policies**
 ![](https://main.qcloudimg.com/raw/db9ab2a3e4b2afb1b921686f88078923.png)
5. Enter the accepter CIDR (`10.0.1.0/24`) for the destination, select **Peering Connections** for next hop type, and select the created peering connection (PeerConn) for the next hop.
 ![](https://main.qcloudimg.com/raw/b497dcfd43a2661cd336649f554ddc78.png)
6. Click **OK**. After the route table is configured, the communication can be achieved between different IP address ranges of two VPCs.
**The accepter route table is configured in the same way as that of requester.**

>**Notes:**
>- You must configure routes on both ends before you can communicate via the peering connection.
>- For communication between multiple IP address ranges of two VPCs on both ends, you only need to **increase the corresponding route table entries** instead of creating multiple peering connections.

