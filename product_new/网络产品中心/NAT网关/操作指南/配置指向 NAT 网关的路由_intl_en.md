After creating a NAT gateway, you need to configure routing rules to direct the subnet traffic to the NAT gateway.
1. Click **Route Table** in the left sidebar of [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the route table list, click the route table ID/name associated with the subnet that needs to access the internet.
3. Click **+ New routing policies**.
4. In the pop-up window that appears, enter the destination (the public network access IP range), select **NAT Gateway** for **Next Hop Type**, and then select the created VPN gateway ID for **Next Hop**.
5. After you click **Create** to complete the configuration, the traffic generated when the CVM in the subnet associated with the route table accesses the Internet will be directed to the NAT gateway.
