## Monthly Subscription
### Alerts
- From seven days before your resource expires until the resource is released, the system will send alerts to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Prepaid Billing > Billing Process](https://intl.cloud.tencent.com/document/product/555/42701).

### Repossession
- The system will send you a renewal notification 7 days before the expiration of database resources.
- After the expiration, your TDSQL-C for MySQL cluster cannot be used and will be put into the recycle bin. You can view and renew the corresponding instances and the cluster on the recycle bin page in the console.
- Resources in the recycle bin will be retained for seven days. If the instance in the recycle bin is not renewed within seven days, it will be repossessed, and all data will be deleted and cannot be recovered.

## Pay-as-You-Go
> !After you stop using pay-as-you-go resources, **terminate them as soon as possible** as instructed in [Deleting Instance](https://intl.cloud.tencent.com/document/product/1098/44628) to avoid fee deduction.
> Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.

### Alerts
- Pay-as-you-go resources are billed for every clock-hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328).


### Overdue payment policy
1. **When your account balance becomes negative:**
   - You can continue to use your TDSQL-C for MySQL cluster in 24 hours. We will continue to bill you for this period.
   - Your TDSQL-C for MySQL cluster will be automatically isolated into the recycle bin after 24 hours, and billing will stop.

2. **After the isolation:**
   - If you top up your account within three days after the isolation to a positive balance, the billing will continue, and the cluster will be automatically recovered for normal use.
   - If your account balance remains negative after three days, the isolated cluster will be deactivated and put into the repossession queue, and all data in it will be cleared and cannot be recovered.
When the cluster is repossessed, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).

