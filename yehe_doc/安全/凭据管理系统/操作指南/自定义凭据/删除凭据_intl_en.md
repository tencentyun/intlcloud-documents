## Note
- SSM provides the schedule deletion feature against accidental secret deletions. Each deletion has **a mandatory waiting period of 0-30 days**, that is, there will be 0-30 days to wait before the deletion becomes permanent.
- Once deleted, a secret **cannot be restored**, and all of its content **cannot be called**.

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm/index) and click **Secret List** on the left sidebar. You can switch between regions in the upper left corner of the page to view secrets in other regions as needed.
2. Select the secret to be deleted on schedule in the **Secret List**. If the secret is enabled, you need to disable it first and then click **Schedule Deletion** in the **Operation** column.
![](https://main.qcloudimg.com/raw/7e9f544403c810ae419d461789b6a96d.png)
3. Set the number of schedule deletion days and then click **Confirm**. The secret will be deleted after the set number of days.
![](https://main.qcloudimg.com/raw/e651915d58d03adde3b2f1789d91497f.png)
>!If the waiting period is set to "0", the secret will be deleted immediately.

4. The deletion of a secret can be canceled within the waiting period (1-30 days). You can click **Cancel Deletion** in the **Operation** column on the right. After the deletion is canceled, the secret key will be restored to the "enabled" status. You can disable, edit, delete, or perform other operations on the secret.
![](https://main.qcloudimg.com/raw/dbdf66930566eadc7f44fe9785ec519a.png)
