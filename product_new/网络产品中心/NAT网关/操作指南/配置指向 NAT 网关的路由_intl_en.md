After creating a NAT gateway, you need to configure routing rules to direct the subnet traffic to the NAT gateway.
1. Click **Route Table** in the left sidebar of [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the route table list, click the route table ID associated with the subnet that needs to access the Internet, to enter the details page. Then, click **New Routing Policies** in **Routing Policies**.
3. In the pop-up window that appears, enter the destination, select **NAT Gateway** for **Next Hop Type**, and then select the created NAT gateway ID for **Next Hop**.
![2](https://main.qcloudimg.com/raw/8921a0084f243ea6edde02087b8c5651.png)
4. After you click **OK** to complete the configuration, the traffic generated when the CVM in the subnet associated with the route table accesses the Internet will be directed to the NAT gateway.
