After the NAT Gateway is created, you need to configure routing policies to direct the subnet traffic to the NAT Gateway.
There are two options:
- Method 1: Configure in the **NAT Gateway** console
- Method 2: Configure in the **Route Table** console

## Directions

### Method 1: Configure in the **NAT Gateway** console
1. Log in to the [**NAT Gateway console**](https://console.cloud.tencent.com/vpc/nat?rid=1).
2. In the NAT gateway list, click the VPC ID of the target NAT gateway.
   ![]()
3. Click **Subnet** in the VPC details page.
   ![]()
4. In the **Subnets** list, find the subnet that needs to access the internet and click the route table ID.
5. Click **+New routing policies** on the **Basic Information** page.
    ![]()
6. In the **Add route** box, enter the destination (public IP range), select **NAT gateway** in **Next hop type** and choose an existing NAT gateway.
    ![]()
7. Click **Create** to complete. 
   


### Method 2: Configure in the **Route Table** console
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Route Tables** on the left sidebar.
2. Locate the route table associated with the subnet that needs to access the Internet, and click its **ID/Name** to enter the details page.
![]()
3. Click **+New routing policies** on the **Basic Information** page.
4. In the **Add route** box, enter the destination (public IP range), select **NAT gateway** in **Next hop type** and choose an existing NAT gateway.
    ![]()
5. Click **Create** to complete. 
