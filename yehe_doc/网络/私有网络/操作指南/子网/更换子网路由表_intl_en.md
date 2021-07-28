Each subnet must be associated with one [route table](https://intl.cloud.tencent.com/document/product/215/31810), which is used to control the outbound traffic direction of the subnet. You can change the Subnet’s associated route table in the **VPC -> Subnet** page according to the routing needs of the subnet. If you need to create a route table, please see [Creating a Custom Route Table](https://intl.cloud.tencent.com/document/product/215/35236).

## Systems impact
Considering that the route table directly impacts the traffic flow in the subnet, any changes such as route table association or route entries must be carefully considered in accordance to the business needs of the network flows.

## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Subnet** in the left sidebar to go to the subnet management page.
3. The system provides two methods to change the route table associated with the subnet.
    + Click **More** > **Change Route Table** in the **Operation** column on the right side of the subnet that needs to change the route table.
        ![](https://main.qcloudimg.com/raw/154c5a6ff6b746a1a593fc4ac6a5ece9.png)
	+ Click the ID of the subnet that needs to change the route table to go to the details page, switch to the **Routing Rules** tab, and click **Change Route Table**.
	    ![](https://main.qcloudimg.com/raw/572762da3d2163b3c30ed07c8a167130.png)
4. In the pop-up window, select a new route table in the drop-down list, confirm the impact on your business, and click **Confirm**.
    ![](https://main.qcloudimg.com/raw/c51606ba642517ffc01bcbf666abab49.png)
