This document will take an example to show your how to implement **intra-account cross-region** communication.
## Example
- IP address range 1: The subnet A `192.168.1.0/24` of VPC1 in **Guangzhou**.
- IP address range 2: The subnet B `10.0.1.0/24` of VPC2 in **Beijing**.

Follow the two steps below to implement communication between IP address range 1 and 2 over a peering connection under the same account. Refer to the following for specific operations.
![](//mc.qcloudimg.com/static/img/4817a68077ccf82022ea167476871c41/3.jpg)

## Step 1: Create a Peering Connection
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> **Virtual Private Cloud** to go to the VPC console.
2. In the left pane, click **Peering Connections** to go to the management page.
3. Select the region and the VPC (e.g. Guangzhou and `VPC1`) above the list, and then click **New** to create a peering connection.
 ![](https://main.qcloudimg.com/raw/57786db314c63e45265a9656d6ef4671.png)
4. Enter a name (e.g. PeerConn), select the requester region and network, and the accepter region (such as Beijing), account type and VPC. Accept the service agreement.
 - If the accepter account type is **My Account**, choose from the drop-down list.
 - If the accepter account type is **Other accounts**, enter the account ID and VPC ID of the accepter account.
 ![](https://main.qcloudimg.com/raw/c3ff3d9eb69255f5b1587edab7a13d23.png)
5. Select the bandwidth cap.
 - For an intra-region peering connection, there is no restriction on the bandwidth, so this **cannot be modified**.
 - For a cross-region peering connection, you can select a bandwidth cap. If you need a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
6. Click **Create**. A peering connection between the VPCs under the same account takes effect immediately after its creation.


## Step 2: Set Route Tables on Both Ends
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


