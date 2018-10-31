After the creation of an NAT gateway, you need to configure the routing rules to direct the subnet traffic to the NAT gateway.
1. In the left pane on the VPC console, click **Route Tables**.
2. In the route table list, click the route table ID associated with the subnet that needs to access the Internet to enter the details page, and then click **New Routing Policies** in **Routing Policies**.
 ![2](https://main.qcloudimg.com/raw/86d1a69fd07814a4dc7230420ea154c5.png)
3. In the pop-up box, enter the destination, select **NAT Gateway** for **Next Hop Type**, and then select the created VPN gateway ID for **Next Hop**.
 ![](https://main.qcloudimg.com/raw/4d48231dac7395c88600884983ba5bd9.png)
4. After you click **Create** to complete the configuration, the traffic generated when the CVM in the subnet associated with the route table accesses the Internet will be directed to the NAT gateway.
