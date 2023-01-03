## Pay-as-You-Go TencentDB Instance
> !After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deductions.
> Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.
### Alerts
- Pay-as-you-go resources are billed for every clock-hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328).

### Processing for overdue payments
1. **When your account balance becomes negative:**
   - You can continue to use your database for 24 hours from the moment your account becomes negative. We will also continue to bill you for this period.
   - When your account has been in arrears for 24 hours, **your TencentDB instance will automatically shut down**, and the billing will stop.

2. **After automatic shutdown:**
   - Within 7 days after automatic shutdown, If you top up your account to a positive balance, you can start up the instance, and the billing will continue; otherwise, it cannot be started up.
   - After 7 days of shutdown, TencentDB instances will be repossessed by Tencent Cloud. All data will be deleted and cannot be recovered. The system will send a notification to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods.

![](https://qcloudimg.tencent-cloud.cn/raw/ee98fae4c665cb2427408b179a9a2231.png)

