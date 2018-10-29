You can access the Internet through an NAT gateway by following the steps below.
## Step 1: Create an NAT gateway
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), select **Cloud Products** -> **Virtual Private Cloud** to go to the VPC console, and then click **NAT Gateway** on the left pane.
2. Click **New** at the upper left corner.
 ![0](https://main.qcloudimg.com/raw/7c78b71c0389a94596e8cdae0cb108fa.png)
Enter or confirm the following parameters in the pop-up box:
 - Gateway Name;
 - Gateway Type (which can be modified);
 - Network: VPC of NAT gateway service;
 - Elastic IPs: Bind an EIP to the NAT gateway. You can select an existing EIP, or purchase and bind a new EIP.
  ![1](https://main.qcloudimg.com/raw/a57f4f32b6f6b8df7e9d54399816519e.png)
3. After selection, click **Create** to create the NAT gateway.

>**Note:**
>The rental fee will be frozen for 1 hour during the creation of a NAT gateway.

## Step 2: Configure the route table associated with the subnet
After the creation of an NAT gateway, you need to configure the routing rules to direct the subnet traffic to the NAT gateway.
1. In the left pane on the VPC console, click **Route Tables**.
2. In the route table list, click the route table ID associated with the subnet that needs to access the Internet to enter the details page, and then click **New Routing Policies** in **Routing Policies**.
 ![2](https://main.qcloudimg.com/raw/86d1a69fd07814a4dc7230420ea154c5.png)
3. In the pop-up box, enter the destination, select **NAT Gateway** for **Next Hop Type**, and then select the created VPN gateway ID for **Next Hop**.
 ![](https://main.qcloudimg.com/raw/493c0d9742a883f57e35548215e73f44.png)
4. After you click **Create** to complete the configuration, the traffic generated when the CVM in the subnet associated with the route table accesses the Internet will be directed to the NAT gateway.

## Step 3: Enable gateway traffic control (optional)
If "Gateway Traffic Control" is enabled, you can view details of traffic going through an NAT gateway from all IPs over the last 7 days, and set the outbound bandwidth cap for the traffic from an IP to the specified NAT gateway.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), select **Products** -> **Virtual Private Cloud* to go to the VPC console, and then click **NAT Gateway** on the left pane.
2. In the list page, select the NAT gateway for which you want to enable gateway traffic control to go to its details page.
3. Click **Monitor** in the tab, and then enable **Gateway Traffic Control** at the upper right corner.
After the "Gateway Traffic Control" is enabled, it takes 5 to 6 minutes to collect and publish data. And then you can view the monitoring details and graphs.
 ![](https://main.qcloudimg.com/raw/2a515b83a50ae293c4159242a3327757.png)
 
 >**Note:**
 For more information about gateway traffic control, see [Set Gateway Traffic Control](/document/product/552/18242) and [View Gateway Traffic Control Details](/document/product/552/18239).


