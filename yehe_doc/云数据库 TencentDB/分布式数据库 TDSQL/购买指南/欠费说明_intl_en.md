## Expiration Reminder for Pay-as-You-Go TencentDB Instances
![](https://main.qcloudimg.com/raw/416582107bb3a3db9a40f8d194e23426.png)

### Balance reminder
We will estimate the number of days it takes your account balance to become negative based on the usage in the past 24 hours and current balance. If it is less than five days, we will send a reminder to your Tencent Cloud account creator and all the collaborators through email and SMS.

### Arrears reminder
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative (point 1 in the figure above), we will notify the Tencent Cloud account creator and all the collaborators through email and SMS.

### Arrears processing
**Starting from the moment your account becomes negative:**
- You can continue to use your TencentDB instance for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period.
- When your account is in arrears for 2 hours (point 2 in the figure above), **your TencentDB instance will automatically shut down. We will also stop billing you for service**.

**After automatic shutdown:**
- Within 24 hours after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database. If your balance is positive, the billing continues, and you can start your database.
- If your account remains negative for 24 hours after shutdown (point 3 in the figure above), the pay-as-you-go TencentDB instance will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all the collaborators through email and SMS when the TencentDB instance is repossessed.
>When you no longer use pay-as-you-go resources, **terminate them as soon as possible** to avoid further fee deductions.
> After the TencentDB instance is terminated or repossessed, the data will be deleted and cannot be recovered.
> As your actual resource consumption may change over time, there may be some deviation in the balance alert.
