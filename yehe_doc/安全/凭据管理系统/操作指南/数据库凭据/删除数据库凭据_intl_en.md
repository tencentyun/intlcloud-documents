## Note
- SSM provides the schedule deletion feature against accidental secret deletions. Each deletion has **a mandatory waiting period of 0-30 days**, that is, there will be 0-30 days to wait before the deletion becomes permanent.
- Once deleted, a secret **cannot be restored**, and all of its content **cannot be called**.

## Directions
1. Log in to the [SSM Console](https://console.cloud.tencent.com/ssm) and click **Database Credential** on the left sidebar.
 ![](https://main.qcloudimg.com/raw/485fa47ea3688c234a97ebb1d6b8f9be.png)
2. Click the drop-down button in the top left corner of the credential list to modify the region.
   ![](https://main.qcloudimg.com/raw/685d60e0fbaf7e0787a0afb2d4510fb7.png)
3. In the search box on the right, enter the full or partial name of the credential you want to search.
   ![](https://main.qcloudimg.com/raw/1ee7a145a0106cd3368a9ff50aa254f2.png)
4. Select a credential you schedule to delete and then click **Schedule Deletion** in the **Operation** column.
>?If the credential is enabled, you need to disable it first by clicking **Disable**.

![](https://main.qcloudimg.com/raw/98e37565bad5c4b1e8d59fc032c1a287.png)
5. Set the number of schedule deletion days and then click **Confirm**. The credential will be deleted after the set number of days.
>!If the waiting period is set to "0", the credential will be deleted immediately.

![](https://main.qcloudimg.com/raw/990bce72794c343f680ac72f1e9e8d9b.png)
6. Within the 1-30 waiting period, you can cancel the schedule deletion. To cancel it, click **Cancel Deletion**.
![](https://main.qcloudimg.com/raw/1d47e51e6d15c9c3bcad955b691cf11a.png)
7. Enable the credential you just disabled for cancelling the deletion. Now you can disable, edit and delete the credential again.
