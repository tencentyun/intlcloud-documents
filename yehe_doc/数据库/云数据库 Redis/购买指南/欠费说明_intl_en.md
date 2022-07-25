

## Pay-as-You-Go

>!
> After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
> As your actual resource consumption may change over time, there may be some deviation in the balance alert.

### Alerts

- Pay-as-you-go resources are billed on the hour. When your account balance becomes negative, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, and other methods as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).
- For more information on the message notification mechanism, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328).

### Overdue payment policy

1. **When your account balance becomes negative:**
   - You can continue to use your TencentDB instance for 24 hours. We will continue to bill you for this period.
   - After 24 hours, the TencentDB instance will be automatically shut down and isolated into the recycle bin, and the billing will stop.
2. **After automatic shutdown:**
   - If the overdue payment is paid within 24 hours, you can start the instance up for use. For detailed directions, see Restoring Isolated Instance.
   - After 24 hours of shutdown, the TencentDB instance will be repossessed by Tencent Cloud. All data will be erased and cannot be recovered. Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email, SMS, etc.


