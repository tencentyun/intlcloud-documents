The collected log data of FL needs to be delivered to CLS. Therefor, you need to grant permissions to FL to access CLS. Otherwise, you will be unable to query the log data in CLS. This document describes how to grant permissions for FL to access CLS.

## Directions
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).
2. Click **Role** to go to the role management page.
![]()
3. Click **Create a role** and select **Tencent Cloud Account** as the role entity.
![]()
4. Select **Other root account** as the type, and enter the account number “91000000202”. Then, click **Next**.
![]()
5. Enter “CLS” in the search box. Select “QcloudCLSFullAccess” and click **Next**.
![]()
6. Enter the role name “FlowLogClsRole”.
![]()
7. Click **Ok**. The role authorization is successful as shown in the figure below.
![]()
