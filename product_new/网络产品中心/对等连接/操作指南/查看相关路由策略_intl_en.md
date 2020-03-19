1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) and choose **Products** > **Networking** > **Virtual Private Cloud** to access the Virtual Private Cloud (VPC) console.
2. In the left sidebar, click **Peering Connections** to go to the management page.
3. Select a region and a VPC above the list.
4. Click the ID of the target peering connection to go to its details page.
5. Check the following items in the related routing policy: the next hop corresponding to the destination IP range, the associated subnet, and the related route table of the peering connection.


>**Note:**
>If you have created a peering connection but cannot communicate over it, check whether the route tables at **both ends** are correctly configured by following the above steps.
