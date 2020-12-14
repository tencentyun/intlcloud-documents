After a CCN instance is created and associated with network instances, you need to configure a bandwidth limit in both associated regions to enable communications. For a monthly-subscribed CCN instance, you also need to purchase bandwidth for the regions. Please note that the monthly-subscribed CCN instance is currently in beta. To try it out, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

## Prerequisites
- You have created a CCN instance and associated it with network instances as instructed in [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062) and [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
- Check that there is no route conflict in the route table. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).

## Purchasing Bandwidth (for Monthly-subscribed CCN Instances)
If you create a monthly-subscribed CCN instance with default bandwidth, you can use a bandwidth of 10 Kbps free of charge in all regions. If you require a higher bandwidth, please purchase bandwidth in the regions to enable communications.
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Cloud Connect Network** in the left sidebar.
2. On the CCN instance list page, click the **ID/Name** of the target monthly-subscribed CCN instance to enter its details page. Click the **Bandwidth Management** tab.
3. On the **Bandwidth Management** page, click **Purchase Bandwidth**. Perform the following operations in the pop-up window.
    1. Select the two regions associated with the CCN instance, and configure the bandwidth limit and usage period.
    >? A bandwidth up to 10,000 Mbps can be configured.
    >
    ![](https://main.qcloudimg.com/raw/325b8eaef7cdd0783a9a0fc00aec35db.png)
    
    2. Click **Confirm**.
 
## Configuring Inter-region Bandwidth Limit (for Pay-as-you-go CCN Instances Billed by Monthly 95th Percentile)
You can configure the inter-region bandwidth limit for pay-as-you-go CCN instances to control the bandwidth costs.
> ?The default bandwidth cap is 1 Gbps. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
> 
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Cloud Connect Network** in the left sidebar.
2. On the CCN instance list page, click the **ID/Name** of the target pay-as-you-go CCN instances to enter its details page. Click the **Bandwidth Management** tab.
3. Configure the bandwidth limit depending on the speed limit mode of the CCN instance:
  - Set inter-region bandwidth limit
 Click **Change Bandwidth**. Select **Region A** and **Region B** from the drop-down list, and set the bandwidth cap. You can also click **Add** to configure multiple bandwidth limit rules. After the configuration is complete, click **OK**.
 ![img](https://main.qcloudimg.com/raw/952c27b2590d37f6f14785b12a5d4c2b.png)
  - Set the region outbound bandwidth limit
 Click **Adjust bandwidth speed limit**. In the pop-up window, select desired regions in the **Add region outbound speed limit** list on the left and set the bandwidth cap on the right. Click **OK**.
 ![img](https://main.qcloudimg.com/raw/a961f2724eda0a156304dea7169ae319.png)
4. (Optional) Perform the following steps to change the bandwidth limit type to meet your requirements.
    1. Click **Change** on the right of **Speed limit mode**.
        ![img](https://main.qcloudimg.com/raw/c66d120e44a69834f6f9ca8ee655d328.png)  
    2. Select a bandwidth limit type from the drop-down list in the pop-up window.
        > !Changing the bandwidth limit type will delete existing configurations. The bandwidth cap will be set to 1 Gbps by default. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
        > 
       ![](https://main.qcloudimg.com/raw/93232c58d1e626eaab54685923cc2009.png)
       <table>
			 <tr>
			 <th>Bandwidth Limit</th>
			 <th>Description</th>
			 </tr>
			 <tr>
			 <td>Region bandwidth out</td>
			 <td>The outbound bandwidth cap of a single region to other regions</td>
			 </tr>
			 <tr>
			 <td>Inter-region bandwidth</td>
			 <td>The inbound and outbound bandwidth cap between regions. Monthly-subscribed CCN instances only support inter-region bandwidth limit.</td>
			 </tr>
			 </table>
    3. Click **OK**.
