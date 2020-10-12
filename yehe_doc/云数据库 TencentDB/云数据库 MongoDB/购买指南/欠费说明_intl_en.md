## Expiration Reminder for Pay-as-You-Go Resources
### Balance reminder
We will estimate the number of days it takes for your account balance to become negative based on the past 24 hours usage and current balance under the pay-as-you-go mode. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears reminder
Fees for pay-as-you-go resources are charged by the hour. When your account balance becomes negative, we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

### Arrears processing
**Starting from the moment your account balance becomes negative:**
- You can continue to use your database within 24 hours from the moment your account balance becomes negative. We will also continue to bill you for this period.
- When your account has been in arrears for 24 hours, your database instances will **automatically shut down** and be removed from the instance list and put in to the recycle bin, and we will **stop billing you for this service**.

**After automatic shutdown:**
- Within 3 days after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database; if your balance is positive, the billing continues, and you can start your database.
- If your account balance remains negative for 3 days after shutdown, the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the database is repossessed.
> !
>- When you no longer use pay-as-you-go resources, **terminate them as soon as possible** to avoid additional fees.
>- Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.
>- **You cannot restore pay-as-you-go instances from the recycle bin** if your account is in arrears.

### Account top-up
- After the account is topped up to a positive balance, you can restore instances in the recycle bin.
- Only pay-as-you-go instances can be restored in batches in the recycle bin.

