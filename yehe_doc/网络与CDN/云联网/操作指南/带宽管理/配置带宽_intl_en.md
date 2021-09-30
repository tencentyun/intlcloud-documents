After creating and associating a CCN instance with network instances, you need to configure bandwidth to enable communications. If the CCN billing mode is pay-as-you-go by monthly 95th percentile, configure a bandwidth cap in both regions the CCN instance connects to.

## Prerequisites

- You have created a CCN instance and associated it with network instances as instructed in [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062) and [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).
- Check that there is no route conflict in the route table. For more information, see [Viewing Routing Information](https://intl.cloud.tencent.com/document/product/1003/30066).


## Setting Cross-region Bandwidth Cap (for Pay-as-you-go CCN Instances Billed by Monthly 95th Percentile)

You can configure a cross-region bandwidth cap for pay-as-you-go CCN instances billed by monthly 95th percentile to control the bandwidth costs.

> ?The default bandwidth cap is 1 Gbps. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) and access the CCN management page.

2. On the CCN instance list page, click the **ID/Name** of the target pay-as-you-go CCN instances billed by monthly 95 percentile to enter its details page. Click the **Bandwidth Management** tab.

3. (Optional) Perform the following steps to change the bandwidth limit mode to meet your requirements.

   1. Click **Change** on the right of the **Bandwidth limit mode**.
      ![](https://main.qcloudimg.com/raw/fa211668316de376d3321fe87137e3a4.png)

   2. Select a bandwidth limit mode from the drop-down list in the pop-up window.

      > !Changing the bandwidth limit mode will delete existing configurations. The bandwidth cap will be set to 1 Gbps by default. If you require a higher bandwidth, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
      >
      ![](https://main.qcloudimg.com/raw/d512626f5a9068673fbf2d1e1cc62abc.png)

      <table>
      	 <tr>
      	 <th>Bandwidth Limit</th>
      	 <th>Notes</th>
      	 </tr>
      	 <tr>
      	 <td>Region bandwidth out</td>
      	 <td>The total outbound bandwidth cap from a single region to other regions</td>
      	 </tr>
      	 <tr>
      	 <td>Inter-region bandwidth</td>
      	 <td>The inbound and outbound bandwidth cap between two regions</td>
      	 </tr>
      	 </table>

   3. Click **OK**.

4. Configure the bandwidth cap depending on the bandwidth limit mode of the CCN instance:

  - Set inter-region bandwidth limit
    Click **Change Bandwidth**. In the pop-up window, select **Region A** and **Region B** from the drop-down list and enter the **Bandwidth Cap**. You can also click **Add** to configure multiple bandwidth limit rules, and then click **OK**.
    ![](https://main.qcloudimg.com/raw/5c85f5e688d795af90d7e09bb38d905f.png)
  - Set the region outbound bandwidth limit
    Click **Adjust bandwidth cap**. In the pop-up window, select regions for which you want to limit the bandwidth on the left and set the bandwidth cap on the right. Click **OK**.
    ![img](https://main.qcloudimg.com/raw/2c71d31b0cc2a9bd74f1224083b66cfe.png)

