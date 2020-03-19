1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Subnet** to go to the management page.
3. Click the ID of the route table (route table A) associated with the local subnet (subnet A) of the peering connection to access the route table details page.
4. Click **+ New routing policies**.
5. Enter the peer CIDR block (`10.0.1.0/24`) for the destination, select **Peering Connections** for the next hop type, and select the created peering connection (PeerConn) for the next hop.
 ![](https://main.qcloudimg.com/raw/b497dcfd43a2661cd336649f554ddc78.png)
6. Click **OK**. After the route table is configured, communication is enabled between the IP ranges of the two VPCs.
**The peer route table is configured in the same way as that at the local end.**

>**Notes:**
>- You must configure routes at both ends before you can communicate via the peering connection.
>- To enable communication between multiple IP ranges of the two VPCs at both ends, you simply need to **add the corresponding route table entries**, but not create multiple peering connections.
