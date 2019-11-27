You can access the Internet through a NAT gateway by completing the following steps.
## Step 1: Creating a NAT Gateway
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and choose **Cloud Products** > **Virtual Private Cloud** to go to the VPC console. Then, click **NAT Gateway** on the left.
2. Click *Create* in the upper-left corner.
Fill in or confirm the following parameters in the pop-up window that appears:
 - Gateway Name.
 - Gateway Type (which can be changed).
 - Network: VPC where the NAT gateway service resides.
 - Elastic IPs: Bind an EIP to the NAT gateway. You can select an existing EIP, or purchase and bind a new EIP.
  ![](https://main.qcloudimg.com/raw/6ccdfa495f976947f079e32a57223448.png)
3. After selection, click **Create** to create the NAT gateway.

>A rental fee for 1 hour will be frozen during the creation of the NAT gateway.

## Step 2: Configuring the Route Table Associated with the Subnet
After the NAT gateway is created, you need to configure routing policies to direct the subnet traffic to the NAT gateway.
1. In the left sidebar in the VPC console, click **Route Tables**.
2. In the route table list, click the route table ID associated with the subnet that needs to access the Internet to enter the details page. Then, click **Add Routing Policies** in **Routing Policies**.
3. In the pop-up window that appears, enter the destination (the public IP range to be accessed), select **NAT Gateway** for **Next Hop Type**, and then select the created VPN gateway ID for **Next Hop**.
 ![3](https://main.qcloudimg.com/raw/c5a27147477000a932b4060c1a12cba3.png)
4. After you click **Create** to complete the configuration, the traffic generated when the CVM in the subnet associated with the route table accesses the Internet will be directed to the NAT gateway.

## Step 3: Enabling Gateway Traffic Monitoring and Control (Optional)
If **Gateway Traffic Monitoring and Control** is enabled, you can view the metrics of IP traffic flowing through a NAT gateway over the last 7 days, and set an outbound bandwidth for the traffic flowing from an IP address to the specified NAT gateway.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and choose **Products** > **Virtual Private Cloud** to go to the VPC console. Then, click **NAT Gateway** in the left sidebar.
2. In the list page, click the ID of the NAT gateway for which you want to enable Gateway Traffic Monitoring and Control to go to its details page.
3. Open the **Monitoring**tab, and enable **Gateway Traffic Monitoring and Control** in the upper-right corner.
After **Gateway Traffic Monitoring and Control** is enabled, it takes 5 to 6 minutes to collect and publish data. After that, you can view detailed monitoring graphs.
 ![](https://main.qcloudimg.com/raw/303636f1463bcfbd9fcf376f3da19739.png)
 >For more information, see Configuraing Gateway Traffic Monitoring and Control and Viewing Gateway Traffic Monitoring and Control.

