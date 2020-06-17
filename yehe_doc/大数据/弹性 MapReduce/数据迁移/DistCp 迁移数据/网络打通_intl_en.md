## Migrating Files in Local Self-Built HDFS to EMR
The migration of files in a local self-built HDFS to an EMR cluster requires a Direct Connect line for network connectivity. You can contact the developers for assistance.

## Migrating Files in Self-Built HDFS in CVM to EMR
- If the network where the CVM instance resides and the one where the EMR cluster resides are in the same VPC, the files can be transferred freely.
- Otherwise, a peering connection is required for network connectivity.

### Using a peering connection
IP range 1: Subnet A 192.168.1.0/24 in VPC1 of Guangzhou.
IP range 2: Subnet B 10.0.1.0/24 in VPC2 of Beijing.

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Cloud Products** > **Networking** > **Virtual Private Cloud** in the top navigation bar.
2. In the VPC Console, go to the "Peering Connections" page, select the region "Guangzhou" in the list at the top, select "VPC1", and click **+Create**.
![](https://main.qcloudimg.com/raw/5243343aeda2c4704473cb5545a3fbe0.png)
3. Go to the peering connection creation page.
 - **Name**: enter the name of the peering connection, such as PeerConn.
 - **Local Region**: enter the local region, such as Guangzhou.
 - **Local Network**: enter the local network, such as VPC1.
 - **Opposite Account Type**: enter the account of the opposite network. If the two networks in Guangzhou and Beijing are under the same account, select **My account**; otherwise, select "Another account".
 >If both the local network and the opposite network are in the same region (e.g., Guangzhou), the communication is free of charge, and there is no need to select the **bandwidth upper limit**; otherwise, fees will be incurred and the upper limit for bandwidth can be set.
 - **Opposite Region**: enter the opposite region, such as Beijing.
 - **Opposite Network**: enter the opposite network, such as VPC2.
![](https://main.qcloudimg.com/raw/db6f724672169e44f45bd1e1af9fb40d.png)
4. A peering connection between VPCs under the same account takes effect immediately after creation; otherwise, it can take effect only after the opposite account accepts it.
5. Configure the local and opposite route tables for the peering connection.
 - Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Cloud Products** > **Networking** > **Virtual Private Cloud** to enter the VPC Console. Click **Subnet** on the left sidebar to enter the management page. Click the ID of the route table associated with the specified subnet (e.g., subnet VPC1 in Guangzhou) on the local end of the peering connection to enter the route table details page.
![](https://main.qcloudimg.com/raw/e858f68b515b1e9645cb782245091db7.png)
 - Click **+Create Routing Policy**.
 ![](https://main.qcloudimg.com/raw/cfbccd948b73c37fa0c3763eca73f6cc.png)
 - Enter the opposite CIDR (for example, the CIDR of VPC2 in Beijing is 10.0.1.0/24) for the destination, select **Peering connection** for the next hop type, and select the created peering connection (PeerConn) for the next hop.
 ![](https://main.qcloudimg.com/raw/badee3ed07b455ad140eebfb0cdcd2ae.png)
 - You've configured the route table from Guangzhou VPC1 to Beijing VPC2 in the previous steps. Now you need to repeat the steps above to configure the route table from Beijing VPC2 to Guangzhou VPC1.
 - After the route tables are configured, different VPC IP ranges can communicate with each other.
