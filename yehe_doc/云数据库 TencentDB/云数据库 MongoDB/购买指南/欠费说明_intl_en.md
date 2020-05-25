## Expiration Reminder for Pay-as-You-Go Resources
### Balance reminder
We will estimate the number of days it takes for your account balance to become negative based on the past 24 hours usage and current balance under the pay-as-you-go mode. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears reminder
Fees for pay-as-you-go resources are charged by the hour. When your account balance becomes negative, we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears processing
**Starting from the moment your account balance becomes negative:**
- You can continue to use your database within 24 hours from the moment your account balance becomes negative. We will also continue to bill you for this period.
- When your account is in arrears for 24 hours, **your database instance will automatically shut down. We will also stop billing you for service**.

**After automatic shutdown:**
- Within 3 days after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database; if your balance is positive, the billing continues, and you can start your database.
- If your account balance remains negative for 3 days after shutdown, the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the database is repossessed.
> !When you no longer use pay-as-you-go resources, **terminate them as soon as possible** to avoid additional fees.
> Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.

