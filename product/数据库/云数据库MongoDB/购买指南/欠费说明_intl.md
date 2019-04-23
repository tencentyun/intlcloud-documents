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

