## Overview
SSM uses the schedule deletion feature to prevent the accidental deletion of a secret. Each deletion operation has a mandatory waiting period of 0-30 days. That is, after the deletion is confirmed, the secret will be deleted after 0-30 days.
>!Once deleted, a secret cannot be restored, and all of its content cannot be called.
## Directions
1. Log in to the [SSM console](https://console.cloud.tencent.com/ssm/index) and click **Credential List** in the left sidebar. You can switch between regions on the upper left corner of the page to view secrets in other regions as needed.
2. Select the secret to be deleted on schedule in the **Credential List**. If the secret is enabled, you need to disable it first and then click **Schedule Deletion** in the **Operation** column.
![](https://main.qcloudimg.com/raw/3e6122f1050704140352ac8fb933d92f.png)
3. Set the number of schedule deletion days and then click **Confirm**. The secret will be deleted after the set number of days.
![](https://main.qcloudimg.com/raw/9555c59460c2e7328724556d0a4821f2.png)
>!If the waiting period is set to "0", the secret will be deleted immediately.

4. The deletion of a secret can be canceled within the waiting period (1-30 days). You can click **Cancel Deletion** in the **Operation** column on the right. After the deletion is canceled, the secret key will be restored to the "enabled" status. You can disable, edit, delete, or perform other operations on the secret.
![](https://main.qcloudimg.com/raw/0b90440330672f372a87342c6205a6ce.png)
