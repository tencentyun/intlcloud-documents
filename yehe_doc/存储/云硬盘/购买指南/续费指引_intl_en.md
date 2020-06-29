Based on their lifecycles, cloud disks can be used as system disks or data disks of CVMs. The timely renewal of cloud disks can prevent data loss caused by expiration. We recommend that you configure expiration reminders for key data.


## Renewing data disks
- Only CBS data disks with the monthly subscription billing mode support renewal.
- Before a CBS data disk expires, you can renew it to avoid disk unmounting and read/write failure caused by expiration.
- After a CBS data disk expires and before it is terminated (within 14 days after expiration), you can restore it. If you do not renew the disk in time, it will be terminated and may cause data loss.

### Renewing via the console

1. Log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs).
2. Locate the cloud disk and click **Renew**.
3. On the renewal page, choose the renewal period, click **OK**, and complete the payment.

### Renewing via the API
You can use the RenewDisk API to renew elastic cloud disks.

### Restoring via the console

1. Log in to the [CBS Recycle Bin](https://console.cloud.tencent.com/cvm/recycle/cbs).
2. Locate the cloud disk and click **Restore**.
3. Complete the payment.
 You can log in to the [CBS console](https://console.cloud.tencent.com/cvm/cbs) to view the restored resources.