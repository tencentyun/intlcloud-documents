Each subnet must be associated with one [route table](https://intl.cloud.tencent.com/document/product/215/31810), which is used to control the outbound traffic direction of the subnet. You can change the route table associated with the subnet in real time in the **Subnet** page on the VPC console based on the actual business needs. If you need to create a route table, please see [Creating a Custom Route Table](https://intl.cloud.tencent.com/document/product/215/35236).

## Impact on the System
After the route table is replaced by a new one, all instances in the subnet will enable the new route table policy. Please carefully evaluate the business impact.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Subnet** in the left sidebar to go to the subnet management page.
3. The system provides two methods to change the route table associated with the subnet.
    + Click **More** > **Change Route Table** in the **Operation** column on the right side of the subnet that needs to change the route table.
        ![](https://main.qcloudimg.com/raw/5782077dea3fe147112e7ccdd68fae93.png)
	+ Click the ID of the subnet that needs to change the route table to go to the details page, switch to the **Routing Rules** tab, and click **Change Route Table**.
	    ![](https://main.qcloudimg.com/raw/13a97eecd61be194c3d59c312fae487b.png)
4. In the pop-up window, select a new route table in the drop-down list, confirm the impact on your business, and click **Confirm**.
    ![](https://main.qcloudimg.com/raw/be259e098bfe0cbd28e825f8ceaef6f7.png)
