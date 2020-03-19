Both cross-region and cross-account communication of VPCs are advanced features of peering connections. This document describes how to implement **cross-account** communication by using an example.
## Example
- IP range 1: subnet A `192.168.1.0/24` of VPC1 in **Guangzhou**.
- IP range 2: subnet B `10.0.1.0/24` of VPC2 in **Beijing**.

Perform the three steps below to create a peering connection cross different accounts and implement communication between IP ranges 1 and 2:
![](//mc.qcloudimg.com/static/img/4817a68077ccf82022ea167476871c41/3.jpg)

## Step 1: create a peering connection
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Peering Connections** to go to the management page.
3. Select a region and a VPC (for example, Guangzhou and `VPC1`) above the list and then click **New** to create a peering connection.
4. Enter a name (for example, PeerConn) and select the peer region (for example, Beijing), account type, and peer VPC (`VPC2`).
 - If the peer account type is **My Account**, select the account from the drop-down list.
 - If the peer account type is **Other Accounts**, enter the account ID and VPC ID of the peer account.
 ![](https://main.qcloudimg.com/raw/a5e601765747a100a60e7845bf2553b8.png)
5. Select the bandwidth cap.
 - For an intra-region peering connection, there is no bandwidth cap. Therefore, this **cannot be modified**.
 - For a cross-region peering connection, the bandwidth cap can be selected. If you need higher cross-region bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
6. Click **Create**. A peering connection between two VPCs under the same account takes effect immediately after its creation.


## Step 2: accept the peering connection
If VPC2 belongs to another user, you need to notify the user to accept your peering connection request.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Peering Connections** to go to the management page.
3. Select the corresponding region (for example, Beijing) above the list, find the target peering connection (`PeerConn`) in the list, and click **Accept**.
![](
https://main.qcloudimg.com/raw/f7e08e9be4e1c4031989181e20099967.png)
>**Note:**
>After the peering connection is created, you need to add routes that point to the peering connection in both VPCs to enable mutual access between them.

## Step 3: set route tables at both ends
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Subnet** to go to the management page.
3. Click the ID of the route table (route table A) associated with the local subnet (subnet A) of the peering connection to access the route table details page.
4. Click **+ New routing policies**.
5. Enter the peer CIDR block (`10.0.1.0/24`) for the destination, select **Peering Connections** for the next hop type, and select the created peering connection (PeerConn) for the next hop.
 ![](https://main.qcloudimg.com/raw/b497dcfd43a2661cd336649f554ddc78.png)
6. Click **OK**. After the route table is configured, communication is enabled between the IP ranges of the two VPCs.
**Follow the same process as above to configure the peer route table.**

>**Notes:**
>- You must configure routes at both ends before you can communicate via the peering connection.
>- To enable communication between multiple IP ranges of the two VPCs at both ends, you simply need to **add the corresponding routes**, but not create multiple peering connections.

