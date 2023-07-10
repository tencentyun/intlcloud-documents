Based on their lifecycles, cloud disks can be used as system disks or data disks of CVMs. The timely renewal of cloud disks can prevent data loss caused by expiration. We recommend that you configure expiration reminders for key data.


## Renewing data disks
- Only CBS data disks with the monthly subscription billing mode support renewal.
- Before a CBS data disk expires, you can renew it to avoid disk unmounting and read/write failure caused by expiration.
- After a CBS data disk expires and before it is terminated (within 14 days after expiration), you can restore it. If you do not renew the disk in time, it will be terminated and may cause data loss.

### Renewing via the API
You can use the RenewDisk API to renew elastic cloud disks.
