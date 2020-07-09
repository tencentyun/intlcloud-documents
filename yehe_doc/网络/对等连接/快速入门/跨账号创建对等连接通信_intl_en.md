Both cross-region and cross-account communication of VPCs are advanced features of peering connections. This document describes how to implement **cross-account** communication by using an example.
## Example
- IP range 1: subnet A `192.168.1.0/24` of VPC1 in **Guangzhou**.
- IP range 2: subnet B `10.0.1.0/24` of VPC2 in **Beijing**.

Perform the three steps below to create a peering connection across different accounts and implement communication between IP ranges 1 and 2:
![](https://main.qcloudimg.com/raw/b19013471a562535c68a789abf0b9148.jpg)

## Step 1: create a peering connection
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Peering Connections** to go to the **Peering Connections** page.
3. Select a region and a VPC (for example, Guangzhou and `VPC1`) above the list and then click **+New** to create a peering connection.
4. Enter a name (for example, PeerConn) and select the peer region (for example, Beijing), peer account type, and peer network (`VPC2`).
 - If the peer account type is **My Account**, select an account from the drop-down list.
 - If the peer account type is **Other accounts**, enter the account ID and VPC ID of the peer account.
![](https://main.qcloudimg.com/raw/3065957c2797ff7d38f2b8709714b7d7.png)
5. Select the bandwidth cap.
 - For an intra-region peering connection, there is no bandwidth cap. Therefore, this field **cannot be modified**.
 - For a cross-region peering connection, select a bandwidth cap. If you need a higher cross-region bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
6. Click **Create**. A peering connection between two VPCs under the same account takes effect immediately after its creation.


## Step 2: accept the peering connection
If VPC2 belongs to another user, you need to notify the user of accepting your peering connection request.
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Peering Connections** to go to the **Peering Connections** page.
3. Select the target region (for example, Beijing) above the list, locate the peering connection (`PeerConn`) you want to accept, and click **Accept**.
![](https://main.qcloudimg.com/raw/0b3b7123e2826b2b48bcd61acdcf2e27.png)

## Step 3: configure route tables on both sides
>
>- You must configure routes on both sides to implement communication over a peering connection.
>- To enable communication between multiple IP ranges of the two VPCs, you simply need to **add route table entries**, instead of creating multiple peering connections.

1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the left sidebar, click **Subnet** to go to the **Subnet** page.
3. Click a route table (route table A) associated with the local subnet (subnet A) of the peering connection to go to the **Route table**page. Click ID/Name of the route table A to access its details.
4. Click **+ New routing policies**.

5. Enter the peer CIDR (`10.0.1.0/24`) for **Destination**, select **Peering Connections** for **Next hop type**, and select the peering connection created earlier (PeerConn) for **Next hop**.
![](https://main.qcloudimg.com/raw/ce08d68316a267044fe4a23a84644501.png)
6. Click **Create**. After the route table is configured, IP ranges of the two VPCs can communicate with each other.
**Repeat the configuration on the peer route table.**


