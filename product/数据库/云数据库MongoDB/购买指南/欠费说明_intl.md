## Expiration Reminder for Monthly Subscription

### Expiration alert
The system starts sending expiration alerts every other day to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS seven days before the expiration date.

### Arrears alert
The system sends you an arrears alert to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS every other day on and after the expiration date.

### Recycling mechanism
- The system starts sending renewal notifications seven days before the expiration date. 
- You can continue using the cloud services for another seven days after the expiration date, while receiving expiration reminders that remind you to renew the service as soon as possible.
- Starting from the eighth day after the expiration date, you are not allowed to use your database any more. The database will be recycled and stored in the **Recycle Bin**. You still can view the device and renew it on the Recycle Bin page.
- Resources in the recycle bin will be kept for no more than **seven days**. If the renewal had not been done within 7 days, the resource will be recycled by the system, meaning that your databases will be deleted permanently.
- That is, you have a 14-day grace period (**7-day available duration** + **7-day unavailable duration**) after the expiration date. You can opt to renew the service anytime within the grace period. When your balance is sufficient and auto-renewal is enabled, the service will be renewed automatically upon expiration of the subscription.

## Expiration Reminder for Pay-As-You-Go

![](https://mccdn.qcloud.com/img567f91951599d.png)

### Balance alert
The system estimates the length of time during which your resource will remain available based on your consumption and account balance over the past 24 hours. If the estimated time remaining is less than 5 days, the system will send you a balance alert to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Arrears alert
For pay-as-you-go resources, fees are deducted every hour on the hour. When your account balance is negative (Point 1 in the figure above), the system will notify your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Arrears processing
- The database will remain available and billed within **2** hours after the account balance becomes negative.
- After 2 hours (Point 2 in the figure above), the database instance will be automatically shut down and the system will stop charging.
- Within 24 hours after the shutdown, your database instance will be unavailable until your account balance becomes positive. Once your balance becomes positive, the billing will resume and instance will be restarted.
- If your account balance remains negative (Point 3 in the figure above) equal to or more than 24 hours after shutdown, your pay-as-you-go database resource will be recycled and data will be permanently removed from the system.
When recycling the database, the system will notify the Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

>!
> - ** Terminate your pay-as-you-go resource** immediately if you are no longer using it to avoid fees.
> - After the database is terminated or recycled, data will be deleted permanently and cannot be restored.
> - Because your actual resource consumption may change constantly, balance alert may not reflect the most accurate status.

