When no subnet is available, the system will create a default subnet for you in the corresponding region after you purchase an instance (for example, a CVM). The default subnet can help you deploy your business efficiently.

The default subnet has the same features as a custom subnet that you create. In addition, the default subnet does not consume your regional quota. When you no longer need the default subnet, you can delete it by yourself.

## Creating a Subnet
You can create one or more subnets at the same time.
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. Select the region and VPC where the subnet to be created resides and click **+Create**.
4. Enter the subnet’s name, CIDR, availability zone, and associated route table.
![2](https://main.qcloudimg.com/raw/4342b99b376f29713dd9d586c0c9c3ae.png)
5. (Optional) Click **+New Line** to create multiple subnets at a time.
6. Click **Create** to finish the creation.

## Adding CVMs to a Subnet
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. Click the **Add CVM** icon for the subnet where the CVM is to be added.
![](https://main.qcloudimg.com/raw/494ee004004e5a6945af65b3ccf2f34c.png)
4. Complete the purchase of the CVM as instructed on the page. For more information, see the [Purchase Method](https://intl.cloud.tencent.com/document/product/213/506) in the CVM documentation.

## Modifying the Primary Private IP Address of a CVM
Modifying the primary private IP address of a CVM’s primary ENI is supported, but modifying the primary private IP address of a secondary ENI is not supported. The detailed modification procedure is as follows:
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm).
2. Click **Instances** in the left sidebar to go to the management page.
3. Find the CVM to be modified in the list and click the instance ID to go to the details page.
4. Click the **ENI** tab, find the primary IP address to be modified, and click **Modify Primary IP** in the operation column.
![](https://main.qcloudimg.com/raw/71f5e45da54b5047bb515286773043a2.png)
5. In the window that appears, enter the new IP address and click **OK**.
![2](https://main.qcloudimg.com/raw/b12d12eb1f678e4393bd2ec6b94e150a.png)

## Changing the Route Table Associated with a Subnet
Each subnet must be associated with one [route table](https://intl.cloud.tencent.com/document/product/215/4954), which is used to specify the outbound route of the subnet. You can change the route table associated with the subnet in real time. To create a route table, see [Creating a Custom Route Table](https://intl.cloud.tencent.com/document/product/215/35236).
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. In the list, find the subnet for which the route table needs to be changed and click **Change Route Table** in the operation column.
![](https://main.qcloudimg.com/raw/0cff590ca9b028c5084810d80dd48907.png)
4. Choose the route table that needs to be changed from the drop-down list, and then click **OK** to finish the change.
![](https://main.qcloudimg.com/raw/ed4411a2df5bc7d1f8dab86712fd936a.png)

## Deleting a Subnet
> The prerequisites for deleting a subnet are that no IP addresses in the subnet are occupied and that no resources (such as CVMs and TencentDBs) are available in the subnet.

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar to go to the management page.
3. At the top of the list, select the region and VPC to which the subnet to be deleted belongs.
4. In the list, find the row of the subnet to be deleted. Click **Delete** in the operation column and then confirm the deletion.
![](https://main.qcloudimg.com/raw/cbbaa1c8627ad0ed8ed89e817aac546b.png)

## Assigning and Releasing IPv6 CIDR Blocks for a Subnet
>Currently, the IPv6 EIP is in beta test stage. If you do need to use it, please submit a Beta test application.

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **Subnets** in the left sidebar. Select **Region** and **VPC** above the "Subnets" list to display all subnets in your region and VPC.
3. Select a subnet, and click **Obtain IPv6 CIDR**. The system will assign the `/64` IPv6 CIDR block to the subnet. 
![](https://main.qcloudimg.com/raw/c4f222b18ec685f31bcb6dd3b3af12ed.png)
4. Select a subnet that has obtained an IPv6 CIDR block, click **Release IPv6**, confirm the operation, and the system will reclaim the IPv6 CIDR block of the subnet.
![](https://main.qcloudimg.com/raw/99dd050f1e03d4a2bad75a9d14980aab.png)
