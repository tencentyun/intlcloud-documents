## Expiration Reminder for Pay-as-You-Go TencentDB Instances


### Balance reminder
We will estimate the number of days it takes your account balance to become negative based on the usage in the past 24 hours and current balance. If it is less than five days, we will send a reminder to your Tencent Cloud account creator and all the collaborators through email and SMS.

### Overdue payment reminder
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative , we will notify the Tencent Cloud account creator and all the collaborators through email and SMS.

### Overdue payment processing
**Starting from the moment your account becomes negative:**
- You can continue to use your TencentDB instance for 24 hours from the moment your account becomes negative. We will also continue to bill you for this period.
- After your account has been overdue for 24 hours, **your TencentDB instance will automatically shut down. We will also stop billing you for service**.

**After automatic shutdown:**
- If your account is not topped up to a positive balance within 3 days after automatic shutdown, you will not be able to launch your database; If your balance is positive, the billing continues, and you can start your database.
- If your account balance remains negative for 3 days after shutdown, the pay-as-you-go database will be repossessed. **All data will be erased and cannot be retrieved**.

We will notify the Tencent Cloud account creator and all the collaborators through email and SMS when the TencentDB instance is repossessed.
>When you no longer use pay-as-you-go resources, **terminate them as soon as possible** to avoid further fee deductions.
> As your actual resource consumption may change over time, there may be some deviation in the balance alert.
