## Payment Overdue Reminder for Pay-as-You-Go Resources
> !
>- After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
>- Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.
>- If your account has overdue payment, pay-as-you-go instances **cannot be restored** from the recycle bin.
>
### Alerts
- Pay-as-you-go resources are billed on the hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in message subscription in the [Message Center](https://console.cloud.tencent.com/message).


### Processing for overdue payment
**When your account balance becomes negative:**
- TencentDB instances are still available for 24 hours, meanwhile the billing continues.
- After 24 hours, TencentDB instances automatically shuts down and the billing stops. The instances are moved from the instance list to the recycle bin list.

**After automatic shutdown:**
 - If the overdue payment is paid within 3 days, you can start up the instances and the billing continues.
 - After 3 days of shutdown, the TencentDB instances will be repossessed by Tencent Cloud. All data will be erased and cannot be recovered. Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified via email, SMS, etc.

![](https://main.qcloudimg.com/raw/2a4084a3304cd60ede9a2675feda9e97.png)

### Restoring instances after making the payment
- After you make the payment, pay-as-you-go instances in the recycle bin become restorable. Go to the recycle bin list to restore them.
- You can restore instances in batches from the recycle bin, but pay-as-you-go instances and monthly-subscribed instances cannot be restored at the same time.

