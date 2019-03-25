## Expiration Reminder for Monthly Subscription Resources

### Expiration alert
Seven days before the expiration of resources, the system will send you an expiration alert every other day to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Arrears alert
On the day when resources expire and every other day thereafter, the system will send you an arrears alert to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Repossession mechanism
- Seven days before the expiration of cloud services resources, the system will send you a renewal notification. 
- You can continue using the cloud services for an additional period of seven days after the expiration. The system will send you an expiration reminder for the cloud services, and you need to renew them as soon as possible.
- From the eighth day after the expiration, this database cannot be used, and will be put into the **Recycle Bin**. You can view the device and renew it on the Recycle Bin page.
- Resources in the recycle bin will be retained for **seven days**. If the database in the recycle bin is not renewed within 7 days, it will be repossessed by the system. The data will be cleared and cannot be recovered. 
- In other words, there is a **7-day available duration** and a **7-day unavailable duration** for the expired database. Within the 14 days, you can opt to renew the device. If your balance is sufficient and auto-renewal is set for the device, the system will perform renewal automatically upon expiration.

## Expiration Reminder for Pay-as-you-go Resources

![](https://mccdn.qcloud.com/img567f91951599d.png)

### Balance alert
The system estimates the remaining available period of your pay-as-you-go resource based on your usage and account balance over the past 24 hours. If the period is less than 5 days, the system will send you a balance alert to your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Arrears alert
For pay-as-you-go resources, fees are deducted at each o'clock. When your account balance is a negative value (Point 1 in the figure above), the system will notify your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

### Arrears processing
- The database can still be used and billed within **2** hours after the account balance becomes negative.
- After 2 hours (Point 2 in the figure above), the database instance will be automatically shut down and the billing will be stopped.
- Within 24 hours after automatic shutdown, if your account balance is not greater than 0, the database cannot be started up; if your balance is greater than 0, the billing continues and the database can be started up.
- After automatic shutdown, if your account balance remains negative for 24 hours (Point 3 in the figure above), the pay-as-you-go database will be repossessed. In this case, all data will be cleared and cannot be recovered.
When repossessing the database, the system will notify your Tencent Cloud account creator and all the collaborators via internal message, email and SMS.

>!
> - When you do not use a pay-as-you-go resource any longer, **please terminate it in time** to avoid further fee deduction.
> - After the database is terminated or repossessed, the data will be cleared and cannot be recovered.
> - Since your actual resource consumption may change over time, there may be some deviation in the balance alert.

