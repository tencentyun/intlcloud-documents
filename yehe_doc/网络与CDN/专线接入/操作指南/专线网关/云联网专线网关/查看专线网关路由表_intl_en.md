If you use a CCN-based direct connect gateway in the Direct Connect network architecture, you can view the IDC routes and CCN routes to the direct connect gateway on the console.

## Limits
- The route table feature of the direct connect gateway is currently in canary release. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- This feature is unavailable in Taiwan (China) and Canada regions.

## Prerequisites
- You have created a CCN-based direct connect gateway as instructed in [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).
- You have applied for a dedicated tunnel as instructed in [Applying for a Tunnel](https://intl.cloud.tencent.com/document/product/216/19250) and associated with the direct connect gateway.
- You have added IDC IP ranges to the direct connect gateway as instructed in [Adding IDC IP Ranges to the Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/39083).

## Directions
1. Log in to the [Direct Connect Gateway console](https://console.cloud.tencent.com/vpc/dcgw?rid=1).
2. Select a region and VPC at the top of the **Direct Connect Gateway** page. Click the **ID/Name** of the target direct connect gateway to enter its details page.
   ![](https://main.qcloudimg.com/raw/b0eec7cf2c745e961d89836a75a81bb3.png)
3. Select the **Route Table** tab and view the IDC routes and CCN routes to the direct connect gateway. Click <img src="https://main.qcloudimg.com/raw/5be52268cd6656b7fccb91180c187035.svg" style="zoom:10%;" /> to download the route table information.
   ![](https://main.qcloudimg.com/raw/407a1ead3919862370eb6f98640b0c6c.png)
