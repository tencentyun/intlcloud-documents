## Overview
A key cannot be recovered after being deleted, and all data encrypted with it cannot be decrypted. To prevent accidental deletion, KMS adopts a scheduled deletion mechanism, i.e., a mandatory waiting period of 7-30 days is imposed on a deletion operation. Within the waiting period, you can cancel the deletion.

You can log in to the KMS console or call KMS TCCLI to create and cancel a scheduled deletion task. This guide describes how to delete a key in the console.

## Directions
1. Log in to the [KMS Console](https://console.cloud.tencent.com/kms2).
2. Select the key to be deleted, and click **Schedule Deletion** on the right. If the key is enabled, please disable it first.
![](https://main.qcloudimg.com/raw/e72146fde0582c9c0299ab7386bb9cbb.png)
3. Enter the days of waiting period, click **OK**. The key will be deleted as scheduled.
![](https://main.qcloudimg.com/raw/b08c5d89a9754e5cbc36426d7ae2a1be.png)
>! The waiting period can be set to 7-30 days. After being deleted, a key cannot be recovered, and all data encrypted with it cannot be decrypted.
To prevent accidental deletion, the KMS automatic alarm will be triggered:
>- Before a key is deleted, any attempt to call the key will trigger the alarm.
>- The alarm will be triggered every day in the last 3 days before a key is deleted.
4. If you need to cancel the scheduled deletion task, click **Cancel Deletion**. After the key is reset to "Disabled" status, you can enable/modify/delete it or perform other operations.

