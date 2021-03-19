## Migrating Files in a Local Self-built HDFS to EMR
The migration of files in a local self-built HDFS to an EMR cluster requires a direct connection for network connectivity. You can contact Tencent Cloud technical team for assistance.

## Migrating Files in a Self-built HDFS in CVM to EMR
- If the network where the CVM instance resides and the one where the EMR cluster resides are in the same VPC, the files can be transferred freely.
- Otherwise, a peering connection is required for network connectivity.

### Using a peering connection
IP range 1: subnet A 192.168.1.0/24 in VPC1 of Guangzhou.
IP range 2: subnet B 10.0.1.0/24 in VPC2 of Beijing.

1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc), go to the **Peering Connections** page, select the region **Guangzhou** at the top of the list, select **VPC1**, and click **+ New**.
![](https://main.qcloudimg.com/raw/5243343aeda2c4704473cb5545a3fbe0.png)
2. On the peering connection creation page, configure the following fields:
 - **Name**: enter the name of the peering connection, e.g., PeerConn.
 - **Local Region**: enter the local region, e.g, Guangzhou.
 - **Local Network**: enter the local network, e.g., VPC1.
 - **Peer Account Type**: enter the account of the peer network. If the two networks in Guangzhou and Beijing are under the same account, select **My account**; otherwise, select **Other accounts**.
 >?If both the local network and the peer network are in the same region (e.g., Guangzhou), the communication is free of charge, and there is no need to select the bandwidth cap. Otherwise, fees will be incurred and the bandwidth cap can be set.
 - **Peer Region**: enter the peer region, e.g., Beijing.
 - **Peer Network**: enter the peer network, e.g., VPC2.
![](https://main.qcloudimg.com/raw/db6f724672169e44f45bd1e1af9fb40d.png)
4. A peering connection between VPCs under the same account takes effect immediately after creation. If the VPCs are under different accounts, the peering connection takes effect only after the peer account accepts it. For details, see [Creating Intra-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/18836) and [Creating Cross-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/35190).
5. Configure the local and peer route tables for the peering connection.
 - Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/) and select **Products** > **Networking** > **Virtual Private Cloud** to go to the VPC console. Click **Subnet** on the left sidebar to go to the management page. Click the ID of the route table associated with the specified subnet (e.g., subnet VPC1 in Guangzhou) on the local end of the peering connection to go to the route table details page.
![](https://main.qcloudimg.com/raw/e858f68b515b1e9645cb782245091db7.png)
 Click **+ New routing policies**.
 ![](https://main.qcloudimg.com/raw/cfbccd948b73c37fa0c3763eca73f6cc.png)
 - Enter the peer CIDR (for example, the CIDR of VPC2 in Beijing is 10.0.0.1/24) for the destination, select **Peering connections** for the next hop type, and select the created peering connection (PeerConn) for the next hop.
 ![](https://main.qcloudimg.com/raw/badee3ed07b455ad140eebfb0cdcd2ae.png)
 - You've configured the route table from Guangzhou VPC1 to Beijing VPC2 in the previous steps. Now you need to repeat the steps above to configure the route table from Beijing VPC2 to Guangzhou VPC1.
 - After the route tables are configured, IP ranges in different VPCs can communicate with each other.
