This article guides you to use CCN to associate VPCs crossing accounts.

## Prerequisites
- Both accounts are eligible for the [beta testing](https://cloud.tencent.com/apply/p/tp2478t9skn) of the cloud connect network (Here we take account A and B as examples).
- The VPCs to be associated have been created.
- There are no conflicts between the VPC subnet IP range and IDC IP range.

## Step 1: Creating a CCN Instance in Account A
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) using account A, select **Products** -> **Networking** -> **Virtual Private Cloud** to enter the VPC console.
2. Click **Cloud Connect Network** in the left pane to enter the cloud connect network management page.
3. Click **Create**. 
 ![](https://main.qcloudimg.com/raw/4189c3d3af70c389a81159a12198a21c.png)
4. Enter the CCN instance name and notes in the pop-up window.
![](https://main.qcloudimg.com/raw/a1ed83d1e415155a9ff8f255e578d5f8.png)
5. Associate a network instance (or do it after the CCN is created).
6. Click **OK** to create a CCN instance.

## Step 2: Using Account B to Apply for the VPC Association.
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) using account B, select **Products** -> **Networking** -> **Virtual Private Cloud** to enter the VPC console.
2. In the VPC list, click the VPC ID to be associated.
3. In the details page, click **Associate Now**.
![](https://main.qcloudimg.com/raw/ae568a3a69304cf38e83359b25dd5ec9.png)
4. In the pop-up window, select **Other Account** and enter the account A ID and the CCN instance ID.
![](https://main.qcloudimg.com/raw/9a05b970aeb3b22997f56c25b7014b9d.png)
5. Click **OK** to send the association request to the account A.

## Step 3: Accepting the Association Request in Account A
1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com/) using account A, select **Products** -> **Networking** -> **Virtual Private Cloud** to enter the VPC console. 
2. Click **Cloud Connect Network** in the left pane, and then click the ID of the CCN instance with a pending association request. 
3. The **Associate Instance** page shows the information about the VPC to be accepted. Click **Accept** to add the VPC to CCN. 
 ![3](https://main.qcloudimg.com/raw/f63b5f1497e372515521e75f3467eb59.png)

## Step 4: Checking the Route Table
If the IP ranges of the associated network instances conflict, there will be an invalid route. You can check it as follows:
1. In the CCN list, click the CCN ID for which to check the route.
2. In the details page, click **Route Tables** to view the route table.
3. Check if there is any invalid routing policy.
 ![](https://main.qcloudimg.com/raw/ae2fb3be44f2f56ab64a257f505b2b4e.png)
4. For details of routing conflicts, see [Use Limits](https://intl.cloud.tencent.com/document/product/1003/30052#.E8.B7.AF.E7.94.B1.E9.99.90.E5.88.B6). To enable a conflicting route, see [Enabling a Route](https://intl.cloud.tencent.com/document/product/1003/30069).

## Step 5: Setting Cross-region Bandwidth Cap (Optional)
1. In the CCN list, click the CCN ID for which to set the bandwidth.
2. In the details page, click the **Monitoring** tab to view the metrics of the CCN.
3. Select the region for which to set the outbound bandwidth cap.
4. Set the outbound bandwidth cap for each region (1 Gbps by default).
 ![](https://main.qcloudimg.com/raw/e92d2cef0bdf5366054f7fd71415f24a.png)

>Communications between CCN instances incur fees, for pricing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1003/30053).

