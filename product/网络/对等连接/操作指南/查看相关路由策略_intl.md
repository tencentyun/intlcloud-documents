1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Compute & Network** -> **Virtual Private Cloud** to go to the VPC console.
2. In the left pane, click **Peering Connections** to go to the management page.
3. Select the region and VPC above the list.
 ![1](https://main.qcloudimg.com/raw/dc1f8b7f659ed36a8662bf3b5e8f8364.png)
4. Click the ID of the peering connection you want to view to go to its details page.
5. You can find the following in the related routing policy: the next hop information includes the destination IP address range, the associated subnet, and the related route table of the peering connection.
 ![](https://main.qcloudimg.com/raw/64591f21b286f1c12ada66215da8cd1d.png)

>**Note:**
>If you have established a peering connection but cannot communicate over it, check whether the route tables on **both ends** are correctly configured by following the above steps.

