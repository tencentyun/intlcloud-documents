1. Log in to the [CCN console](https://console.cloud.tencent.com/vpc/ccn) and access the CCN management page.
2. Associate a network instance using either of:
 Option 1: associate the network instance on the details page.
     1. Click the **ID/Name** of the desired CCN instance to access the **Associated Instances** page. Click **Add an instance**. 
     2. In the pop-up window, select a network instance type from **VPC**, **Direct Connect Gateway**, **BM Virtual Private Cloud**, and **VPN Gateway**. Select the region to which the network instance belongs and the specific network instance.
>? For CCN to automatically add the routes from the VPN gateway, the VPN gateway for CCN has the VPN tunnel created and SPD policy configured. For more information, see [Connecting IDC to CCN](https://intl.cloud.tencent.com/document/product/1037/36018).
	 3.  (Optional) To associate more network instances, click **Add** and follow the preceding steps.
	 4. Click **OK**. 
         ![](https://main.qcloudimg.com/raw/25969bdf63f77d815c4fa5562bc2ba5d.png)
 Option 2: associate the network instance upon creation.
 When creating a CCN instance, add the network instances to be associated with it.
![](https://main.qcloudimg.com/raw/b72cc7c286f94d8b958def554dfc0150.png)

For more information on creating a network instance, refer to [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805) and [Creating Direct Connect Gateway](https://intl.cloud.tencent.com/document/product/216/19256).

