You can access the public network through a NAT gateway by completing the following steps.
## Step 1: Creating a NAT Gateway
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **+Create** to go to the **Create a NAT Gateway** page. Enter or confirm the following parameters:
 - Gateway Name: name of the gateway

 - Network: VPC where the NAT gateway service resides.

 - Gateway Type: type of the gateway. You can change this later.

 - Outbound Bandwidth Cap: outbound bandwidth limit.

 - Elastic IPs: bind an EIP to the NAT gateway. You can select an existing EIP, or purchase and bind a new EIP.

   ![](https://main.qcloudimg.com/raw/101205d720b9e18a0a5dabca41fc9804.png)
3. Click **Create** to create the NAT gateway.

> The system will freeze an amount equal to the rental fee for one hour when you create a NAT gateway. 

## Step 2: Configuring the Routing Table Associated with the Subnet
After the NAT gateway is created, you need to configure routing policies to direct the traffic of the subnet to the NAT gateway.
1. Click **Route Table** in the left sidebar of the [VPC Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).

2. In the route table list, click the route table ID/name associated with the desired subnet.

   ![](https://main.qcloudimg.com/raw/efe21562a587ab37580a990ba5fbf03d.png)

3. Click **+ New Routing Policies**. The **Add a route** page appears.

4. Enter the destination (the public IP range to be accessed), select **NAT Gateway** for **Next Hop Type**, and then select the ID of the desired NAT gateway **Next Hop**.

   ![](https://main.qcloudimg.com/raw/51573c96993e8349495795a1669e7fdc.png)

5. Click **Create** to complete the configuration. Traffic to the public network from CVM instances in the subnet will now use the NAT gateway.

## Step 3: Enabling Gateway Traffic Monitoring and Control (Optional)
With **Gateway Traffic Monitoring and Control**, you can view the metrics of IP traffic flowing through a NAT gateway over the last 7 days, and set an outbound bandwidth for the traffic flowing from an IP address to the specified NAT gateway.
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc/vpc?rid=1).

2. On the list page, click the ID of the desired NAT gateway to go to its details page.

3. Open the **Monitoring** tab and enable **Gateway Traffic Monitoring and Control** in the upper-right corner.
  After **Gateway Traffic Monitoring and Control** is enabled, it takes 5 to 6 minutes to collect and publish data. After that, you can view detailed monitoring graphs.

  ![](https://main.qcloudimg.com/raw/845c32f8992d39ba33c51b15363a1c04.png)

