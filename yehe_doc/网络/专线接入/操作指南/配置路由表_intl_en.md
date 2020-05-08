After creating a Direct Connect gateway and establishing a dedicated tunnel, you can configure the route table of the VPC instance in the console to direct the desired traffic to the Direct Connect gateway.
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. In the leftside bar, click **Route Tables** to go to the management page.
3. Click the ID of the route table with which you want to associate the Direct Connect gateway to go to the details page.
4. Click **+New Route Policy**.
5. In the window that appears, enter the destination IP range. For the next-hop type, select **Direct Connect gateway**. For the next hop, select the gateway name.
6. Click **OK**.
Now, you can direct the traffic from the specific destination to the Direct Connect gateway to associate it with your on-premises IDC.

