To associate a cross-account VPC, you need to initiate an application on the cross-account VPC end which will then be approved/rejected by the account where the CCN resides. 
The steps are as shown in the figure below:
![0](https://main.qcloudimg.com/raw/c351b9e558517ee4d432f16ef4bd5448.png)
## Applying to Join CCN (in VPC Account)
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console. 
2. Click **Virtual Private Cloud** in the left pane, find the VPC to be joined to CCN and click its ID to enter the details page. 
3. Click **Join CCN**.
 ![1](https://main.qcloudimg.com/raw/a17881a5c0441e3f1e834d8e7e0a0f98.png)
4. In the pop-up, enter the account ID of the peer and the CCN ID and click **OK** to submit the application.
 ![2](https://main.qcloudimg.com/raw/2a9c18546c2a1c0442564ff8445c438c.png)

## Approving the Application (in CCN Account)
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console. 
2. Click **Cloud Connect Network** in the left pane, find the CCN instance for which to approve the application and click its ID to enter the details page. 
3. On the **Associated instances** page, view the information of the VPC for which to approve the application and click **Approve** to join the VPC to the CCN. 
 ![3](https://main.qcloudimg.com/raw/00e77fe68fb24e1de8f3ead93fcbea46.png)

## Checking the Routing Table (Optional)
After the application is approved and the association succeeds, you need to check the routing table to avoid the situation where the route is invalid due to the conflict of IP address range between the instance and an existing instance in the CCN. 
For more information on related operations, see [Checking Routing Table](https://intl.cloud.tencent.com/document/product/1003/31985).

## Setting Cross-domain Interconnection Bandwidth (Optional)
For more information on related operations, see [Setting Cross-domain Interconnection Bandwidth](https://intl.cloud.tencent.com/document/product/1003/30073).
