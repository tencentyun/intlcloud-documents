After the route table is created, it needs to be associated with the subnet in order to control the outbound traffic of the subnet. This document describes how to associate the route table with or disassociate it from the subnet.

## Associating with Subnet
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Route Tables** in the left sidebar to go to the management page.
3. There are two methods to associated with the subnet:
 + In the list, select the route table that needs to associate with the subnet, and click **More** > **Associated Subnets** in the **Operation** column.
![](https://main.qcloudimg.com/raw/1f9b6d2c71865412c527cc157c442ea2.png)
 + Click the route table ID to go to the details page, select **Associated Subnets** tab, and click **+Associate Subnet**.
![](https://main.qcloudimg.com/raw/95d5d37c808f1f273cd73e334f117e81.png)
4. In the pop-up window, select the subnet to associate (a route table can be associated with multiple subnets at the same time, and you can quickly filter by subnet ID/name). Please evaluate the business impact of the association on the subnet. Confirm the impact, and click **OK**.
>!After the route table is associated with the subnet, the original route table associated with the subnet will be replaced with the new one, and the subnet outbound traffic will be executed according to the policies in the new route table. Please carefully evaluate the business impact.
  >
<img src="https://main.qcloudimg.com/raw/159265e6e7d01d2a9645dae8cb74ac71.png" width="70%" />


## Disassociating from Subnet
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Route Tables** in the left sidebar to go to the management page.
3. Click the route table ID to go to the details page, switch to the **Associated Subnets** tab, and click **Disassociate**.
![](https://main.qcloudimg.com/raw/e617445540141ab77fd2982f327ccc15.png)
4. In the pop-up window, select a new route table for the subnet to be disassociated, and click **OK** to complete the disassociation of the current route table from the subnet. The subnet outbound traffic policy will be executed based on the new route table selected for it.
   <img src="https://main.qcloudimg.com/raw/387aebf11bd2089b1c22323b64118afe.png" width="70%" />

