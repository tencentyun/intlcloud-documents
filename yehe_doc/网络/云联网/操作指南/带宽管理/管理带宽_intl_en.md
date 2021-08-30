For a pay-as-you-go CCN instance billed by monthly 95th percentile, you can view its bandwidth cap and change the bandwidth limit type in the console. Please note that the monthly-subscribed CCN instance is currently in beta. To try it out, please [contact sales](https://intl.cloud.tencent.com/contact-sales).

## Prerequisites
- You have created a CCN instance and associated it with network instances as instructed in [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062) and [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
- Check that there is no route conflict in the route table. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).

## Viewing the Bandwidth of Pay-as-you-go CCN Instances Billed by Monthly 95th Percentile
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1) and click **Cloud Connect Network** in the left sidebar.
2. On the CCN instance list page, lick the **ID/Name** of the target pay-as-you-go CCN instance to enter its details page. Click the **Bandwidth Management** tab.
  This tab displays the bandwidth cap of the current bandwidth limit type.
  - Inter-region bandwidth limit
  - Region outbound bandwidth limit
3. (Optional) Change the bandwidth limit type.
  1. Click **Change** on the right of **Speed limit mode**.
  2. Select a bandwidth limit type from the drop-down list in the pop-up window.
  > !Changing the bandwidth limit type will delete existing configurations. The bandwidth cap will be set to 1 Gbps by default. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
  > 
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
			 <td>The inbound and outbound bandwidth cap between regions</td>
			 </tr>
			 </table>
  3. Click **OK**.
