To associate a cross-account VPC, you need to initiate an application on the cross-account VPC end which will then be approved/rejected by the account where the CCN resides. 
The steps are as shown in the figure below:
![0](https://main.qcloudimg.com/raw/60807add361682ba1472ce05ec9095df.png)
## Applying to Join CCN (in VPC Account)
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console. 
2. Click **Virtual Private Cloud** in the left pane, find the VPC to be joined to CCN and click its ID to enter the details page. 
3. Click **Join CCN**.
 ![1](https://main.qcloudimg.com/raw/51fc0718b592f123049a94620567f533.png)
4. In the pop-up, enter the account ID of the peer and the CCN ID and click **OK** to submit the application.
 ![2](https://main.qcloudimg.com/raw/0045ac1991be1bb335a1966814d22686.png)

## Approving the Application (in CCN Account)
1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/) and select **Products** > **Cloud Compute & Network** > **Virtual Private Cloud** to enter the VPC Console. 
2. Click **Cloud Connect Network** in the left pane, find the CCN instance for which to approve the application and click its ID to enter the details page. 
3. On the **Associated instances** page, view the information of the VPC for which to approve the application and click **Approve** to join the VPC to the CCN. 
 ![3](https://main.qcloudimg.com/raw/f63b5f1497e372515521e75f3467eb59.png)

## Checking the Routing Table (Optional)
After the application is approved and the association succeeds, you need to check the routing table to avoid the situation where the route is invalid due to the conflict of IP address range between the instance and an existing instance in the CCN. 
For more information on related operations, see [Checking Routing Table](/document/product/877/18766).

## Setting Cross-domain Interconnection Bandwidth (Optional)
For more information on related operations, see [Setting Cross-domain Interconnection Bandwidth](/document/product/877/18759).
