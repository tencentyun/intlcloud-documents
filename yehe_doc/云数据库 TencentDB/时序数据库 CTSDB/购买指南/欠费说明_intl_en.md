## Expiration Reminder for Pay-as-You-Go TencentDB Instances
### Balance alert
The system estimates the number of days it takes for your account balance to become negative based on the last 24 hours usage and current balance. If it's less than 5 days, we will send a balance alert to your Tencent Cloud account creator and all collaborators via email and SMS.

### Overdue payment alert
For pay-as-you-go resources, fees are deducted on the hour. When your account balance becomes negative, we will notify your Tencent Cloud account creator and all collaborators via email and SMS.

### Overdue payment policy
**Starting from the moment your account balance becomes negative:**
- You can continue to use your TencentDB instance for 24 hours from the moment your account balance becomes negative. We will also continue to bill you for this period.
- When your account has been in arrears for 24 hours, **your TencentDB instance will be automatically shut down, and billing will stop**.

**After automatic shutdown:**
- Within 3 days of automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database; if your balance becomes positive, billing continues, and you can start your database.
- If your account balance remains negative for 3 days after shutdown, the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify your Tencent Cloud account creator and all collaborators via email and SMS when the database is repossessed.
> !After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid fee deduction.
> Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.
