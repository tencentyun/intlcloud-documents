You can easily access the Internet through a NAT Gateway by completing the following steps.
## Step 1. Create a NAT Gateway
>! A rental fee for 1 hour will be frozen upon creation of the NAT Gateway.
>
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?rid=1).
2. Click **+New** in the top-left corner to access the **Create NAT Gateway** page. Enter or confirm the following parameters:
 - Gateway Name: name of the gateway
 - Network: a VPC where the NAT Gateway service resides.
 - Gateway Type: type of the gateway. You can change this later.
 - Outbound Bandwidth Cap: outbound bandwidth limit for the NAT Gateway
 - Elastic IP: select or create an EIP to bind to the NAT Gateway.
>?When the public network is accessed through the EIP bound to a NAT Gateway, the public network traffic is limited by the lower of the NAT Gateway’s or EIP’s bandwidth cap. To ensure that the traffic peak is within the NAT Gateway’s bandwidth cap and avoid packet loss, we recommend:
>- When you create a NAT gateway, the outbound bandwidth cap needs to be smaller or equal to the total bandwidth caps of EIPs to be bound.
>- For an existing NAT Gateway that already bound with an EIP, you can modify the outbound bandwidth cap of the NAT Gateway or EIP, or bind multiple EIPs, ensuring that the outbound bandwidth cap of the NAT Gateway is smaller or equal tothe total bandwidth caps of bound EIPs.
>
![](https://main.qcloudimg.com/raw/101205d720b9e18a0a5dabca41fc9804.png)
3. After completing the configurations, click **Create**.


## Step 2. Configure the Route Table Associated with the Subnet
After the NAT Gateway is created, you need to configure routing policies to direct the subnet traffic to the NAT Gateway.
1. In the NAT gateway list, click the VPC ID of the target NAT gateway.
   ![]()
2. Click **Subnets** in the VPC details page.
   ![]()
3. In the **Subnets** list, find the subnet that needs to access the internet and click the route table ID.
4. Click **+New routing policies** on the **Basic Information** page.
    ![]()
5. In the **Add route** box, enter the destination (public IP range), select **NAT gateway** in **Next hop type** and choose an existing NAT gateway.
    ![](https://main.qcloudimg.com/raw/51573c96993e8349495795a1669e7fdc.png)
6. Click **Create** to complete. 

## Step 3. Enable Gateway Traffic Monitoring Details (Optional)
If **Gateway Traffic Monitoring Details** is enabled, you can view the metrics of IP traffic flowing through a NAT Gateway over the last 7 days, and set an outbound bandwidth of the specified NAT Gateway for traffic from an IP address.
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?rid=1).
2. Locate the NAT Gateway for which you want to enable the gateway traffic monitoring feature, and click the **ID/Name** to enter its details page.
3. Open the **Monitoring** tab, and enable **Gateway Traffic Monitoring** in the upper-right corner.
It will take 5 to 6 minutes to collect and publish data before you can view detailed monitoring graphs. 
<img src="https://main.qcloudimg.com/raw/845c32f8992d39ba33c51b15363a1c04.png" width="60%">

