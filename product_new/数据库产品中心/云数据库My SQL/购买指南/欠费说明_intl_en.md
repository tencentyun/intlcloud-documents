### Repossession Mechanism
- The system will send you a renewal notification 7 days before the expiration of database resources. 
- You can continue using the database for an additional 7 days after the expiration. The system will send you an expiration reminder for the database, and you need to renew it as soon as possible.
- From the eighth day after the expiration, the database cannot be used and will be put into the **recycle bin**. You can view and renew it on the recycle bin page in the console.
- The database will be retained in the recycle bin for up to **seven days**. If you fail to renew it within seven days after it is put into the recycle bin, it will be repossessed by the system, and all the data will be cleared and cannot be recovered. 
- In other words, the database will remain **available for 7 days** after the expiration and become **unavailable for another 7 days**. Within the 14 days, you can choose to renew it. If your balance is sufficient and auto-renewal is set for it, the system will perform renewal automatically upon expiration.

## Expiration Reminder for Pay-as-You-Go TencentDB Instances
![](https://main.qcloudimg.com/raw/282252ac4a40eda999a9a614d8eaaa6a.png)

### Balance Reminder
We will estimate the number of days it takes your account balance to become negative based on the usage in the past 24 hours and current balance. If it is less than five days, we will send a reminder to your Tencent Cloud account creator and all the collaborators via email and SMS.

## Arrears Reminder
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative (Point 1 in the figure above), we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

## Arrears Processing
**Starting from the moment your account becomes negative:**
- You can continue to use your database for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period.
- When your account is in arrears for 2 hours (Point 2 in the figure above), **your database instance will automatically shut down. We will also stop billing you for service**.

**After automatic shutdown:**
- Within 24 hours after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database; If your balance is positive, the billing continues, and you can start your database.
- If your account remains negative for 24 hours after shutdown (Point 3 in the figure above), the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the database is repossessed.
> !When you do not use pay-as-you-go resources any longer, **terminate them as soon as possible** to avoid further fee deduction.
> After the database is terminated or repossessed, the data will be deleted and cannot be recovered.
> Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.
