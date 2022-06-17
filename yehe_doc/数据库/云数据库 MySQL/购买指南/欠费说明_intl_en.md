
## Monthly Subscribed TencentDB Instance
### Alerts
- From seven days before your resource expires until the resource is released, the system will send alerts to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Prepaid Billing](https://intl.cloud.tencent.com/document/product/555/42701).

### Repossession mechanism
- Seven days before the expiration of your TencentDB resources, the system will send you a renewal notification. 
- You can continue using the database for an additional seven days after the expiration. The system will send you an expiration reminder for the database, and you need to renew it as soon as possible.
- From the eighth day after expiration, you will not be able to use your database, which will be put into the **recycle bin**. You can view and renew your database resources on the recycle bin page in the console.
- Resources in the recycle bin will be retained for **seven days**. If the database in the recycle bin is not renewed within seven days, it will be repossessed, and all data will be deleted and cannot be recovered. 
- In other words, there is a **seven-day usable period** and a **seven-day unusable period** for an expired database. Within the 14 days, you can opt to renew at any time. If your balance is sufficient and auto-renewal is enabled, your resources will be automatically renewed upon expiration.

## Pay-as-You-Go TencentDB Instance
>!
>- After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
>- Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.

### Alerts
- Pay-as-you-go resources are billed on the hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328).

### Overdue payment policy
1. **When your account balance becomes negative:**
 - You can continue to use your TencentDB instance for 24 hours. We will continue to bill you for this period.
 - After 24 hours, the TencentDB instance will be automatically shut down, and the billing will stop.

2. **After automatic shutdown:**
 - If the overdue payment is paid within three days, you can start the instances, and the billing will continue.
 - After three days of shutdown, the TencentDB instance will be repossessed by Tencent Cloud. All data will be erased and cannot be recovered. Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email, SMS, etc.

![](https://main.qcloudimg.com/raw/2a4084a3304cd60ede9a2675feda9e97.png)





