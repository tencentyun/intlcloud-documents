## Operation Scenarios
After being deleted, a key cannot be recovered, and all data encrypted with it cannot be decrypted. To prevent accidental deletion, KMS adopts a schedule deletion mechanism, i.e., a mandatory waiting period of 7-30 days is imposed on a deletion operation. Within the waiting period, you can cancel the schedule deletion task.

You can log in to the KMS Console or call KMS TCCLI to create and cancel a schedule key deletion task. This document describes how to delete a key in the console.

## Directions
1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Select the key to be deleted, and click **Schedule Deletion** on the right. If the key is enabled, please disable it first.
![](https://main.qcloudimg.com/raw/e831496edd5ee3af30b7a3ebb83539cd.jpg)
3. Enter the days of waiting period, click **OK**. The key will be deleted as scheduled.
![](https://main.qcloudimg.com/raw/fe2bfc5e05fd921262dc9f46b7ff1314.jpg)
>The waiting period can be set to 7-30 days. After being deleted, a key cannot be recovered, and all data encrypted with it cannot be decrypted.
To prevent accidental deletion, the KMS automatic alarm will be triggered:
>- Before a key is deleted, any attempt to call the key will trigger the alarm.
>- The alarm will be triggered every day in the last 3 days before a key is deleted.
4. If you need to cancel the schedule deletion task, click **Cancel Deletion**. Then, the key will be reset to "Disabled" status. At this point, you can enable/disable/modify/delete it or perform other operations.




