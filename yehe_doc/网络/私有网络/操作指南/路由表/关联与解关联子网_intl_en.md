After the route table is created, it needs to be associated with the subnet in order to control the outbound traffic of the subnet. This document describes how to associate the route table with or unassociate it from the subnet.

## Associating with Subnet
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Route Tables** in the left sidebar to go to the management page.
3. There are two methods to associated with the subnet:
 + In the list, select the route table that needs to associate with the subnet, and click **More** > **Associated Subnets** in the **Operation** column.
![](https://main.qcloudimg.com/raw/0e8f63501b1a2c8c8c99d4f9d838b4e3.png)
 + Click the route table ID to go to the details page, select **Associated Subnets** tab, and click **+Associate Subnet**.
![](https://main.qcloudimg.com/raw/6e814d4f11035afba7f35100ef4bcde6.png)
4. In the pop-up window, select the subnet to associate (a route table can be associated with multiple subnets at the same time, and you can quickly filter by subnet ID/name). Please evaluate the business impact of the association on the subnet. Confirm the impact, and click **OK**.
>!After the route table is associated with the subnet, the original route table associated with the subnet will be replaced with the new one, and the subnet outbound traffic will be executed according to the policies in the new route table. Please carefully evaluate the business impact.

## Disassociating from Subnet
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Route Tables** in the left sidebar to go to the management page.
3. Click the route table ID to go to the details page, switch to the **Associated Subnets** tab, and click **Disassociate**.
![](https://main.qcloudimg.com/raw/077e50e31696c2f9733d3e7030a8e709.png)
4. In the pop-up window, select a new route table for the subnet to be disassociated, and click **OK** to complete the disassociation of the current route table from the subnet. The subnet outbound traffic policy will be executed based on the new route table selected for it.


