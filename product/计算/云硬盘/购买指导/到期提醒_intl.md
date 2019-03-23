
## Arrears Reminder for Postpaid Cloud Disks
 
 ![](https://main.qcloudimg.com/raw/3a50706a27bfc92a2a52d524e04beca9.png)
 
### Balance Reminder
We will estimate the number of days it takes your account balance to become negative based on the past 24 hours usage and current balance. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears Reminder
For postpaid resources, fees are deducted on the hour. When your account balance is in negative (Point 1 in the figure above), we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears Processing

When your account is in arrears for 2 hours (Point 2 in the figure above), your CBS service will be stopped. We will also stop billing you for service.

Within 24 hours after automatic shutdown, if your account is not topped up to a positive balance, you cannot perform read/write operations; If your balance is positive, the billing continues and you can perform read/write operations.

If your account remains negative for 24 hours after shutdown, (Point 3 in the figure above), the postpaid CBS will be repossessed, and all data will be deleted and <font color="red">cannot be recovered</font>.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the postpaid CBS is repossessed.

> Note: 
- When you do not use postpaid resources any longer, **terminate them as soon as possible** to avoid further fee deduction.
- After the resource is terminated or repossessed, the data will be deleted and cannot be recovered.
- Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.
