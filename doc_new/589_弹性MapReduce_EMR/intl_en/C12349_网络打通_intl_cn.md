## Migrating Files in a Local Self-built HDFS to EMR
The migration of files in a local self-built HDFS to an EMR cluster requires a Direct Connect line for network connectivity. You can contact the developers for assistance.

## Migrating Files in a Self-built HDFS in CVM to EMR
- If the network where the CVM instance resides and the one where the EMR cluster resides are in the same VPC, the files can be transferred freely.
- Otherwise, a peering connection is required for network connectivity.

### Using a Peering Connection
IP range 1: Subnet A 192.168.1.0/24 in VPC1 of Guangzhou.
IP range 2: Subnet B 10.0.1.0/24 in VPC2 of Beijing.

1. Log in to the Tencent Cloud Console and select **Products** > **Networking** > **Virtual Private Cloud** in the navigation bar.
2. In the VPC Console, go to the "Peering Connections" page, select the region "Guangzhou" in the list at the top, select "VPC1", and click **Create**.
 ![Create](https://mc.qcloudimg.com/static/img/7f805d799da907e4516ae80c9964779c/6-3-2-2.png)
3. Go to the peering connection creation page.
 - Enter the name of the peering connection as shown in box 1, for example, PeerConn.
 - Enter the local region and network information as shown in box 2, for example, Guangzhou and VPC1.
 - Enter the account of the opposite network as shown in box 3. If the two networks in Guangzhou and Beijing are under the same account, select **My account**; otherwise, select "Another account". It should be noted here that if both the local network and the opposite network are in the same region (e.g., Guangzhou), the communication is free of charge, and there is no need to select the upper limit for bandwidth as shown in box 5; otherwise, fees will be incurred and the upper limit for bandwidth can be set.
 - Enter the opposite region and network as shown in box 4, for example, Beijing and VPC2.
 ![Account](https://mc.qcloudimg.com/static/img/048240b0fab28d71e0dde73892658b45/6-3-2-3.png)
4. A peering connection between VPCs under the same account takes effect immediately after creation; otherwise, it can take effect only after the opposite account accepts it. For more information, see [here](https://cloud.tencent.com/document/product/215/20082).
5. Configure the local and opposite route tables for the peering connection.
 1. Go to the **Subnets** page in the VPC Console.
![Account](https://mc.qcloudimg.com/static/img/1f8371adb83fd1e0532d820b981c7d4e/6-3-2-4.png)
 2. Click "Associated Route Tables" (as shown in the red box above) of the subnet of the local network (e.g., subnet VPC1 in Guangzhou) to enter the route table details page.
 3. Click **Edit** to edit the routing policy. Enter the opposite CIDR (for example, the CIDR of VPC2 in Beijing is 10.0.0.1/24) for the destination, select **Peering connection** for the next hop type, and select the created peering connection (PeerConn) for the next hop.
  ![Account](https://mc.qcloudimg.com/static/img/b613e5d130ef32f27b9dc9da5bbfde8d/6-3-2-5.png)
 4. You’ve configured the route table from Guangzhou VPC1 to Beijing VPC2 in the previous steps. Now you need to repeat the steps above to configure the route table from Beijing VPC2 to Guangzhou VPC1.
 5. After the route tables are configured, different VPC IP ranges can communicate to each other.
