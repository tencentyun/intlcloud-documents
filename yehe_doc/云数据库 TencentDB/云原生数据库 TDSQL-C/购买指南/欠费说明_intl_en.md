## Monthly Subscription
### Alerts
- From seven days before your resource expires until the resource is released, the system will send alerts to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).

### Repossession mechanism
- Seven days before the expiration of your TDSQL-C resources, the system will send you a renewal notification.
- After expiration, your TDSQL-C cluster cannot be used and will be put into the recycle bin. You can view and renew the corresponding instances and the cluster on the recycle bin page in the console.
- Resources in the recycle bin will be retained for seven days. If the database in the recycle bin is not renewed within seven days, it will be repossessed, and all data will be deleted and cannot be recovered.

## Pay-as-You-Go
> !After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deductions.
> Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.


### Alerts
- Pay-as-You-Go resources are billed on the hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).


### Processing for overdue payments
1. **When your account balance becomes negative:**
 - You can continue to use your TDSQL-C cluster for 24 hours. We will continue to bill you for this period.
 - After 24 hours, your TDSQL-C cluster will be automatically isolated into the recycle bin, and the billing will stop.

2. **After the isolation:**
 - If you top up your account within 3 days after the isolation to a positive balance, the billing will continue, and the cluster will be automatically recovered for normal use.
 - If your account balance remains negative after 3 days, the isolated cluster will be deactivated and put into the repossession queue, and all data in it will be cleared and cannot be recovered.
When the cluster is repossessed, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).

