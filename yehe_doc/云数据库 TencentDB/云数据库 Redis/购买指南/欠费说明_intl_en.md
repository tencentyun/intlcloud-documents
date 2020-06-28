## Pay-as-You-Go TencentDB Instances Arrears

### Balance alert

The system estimates the number of days it takes your account balance to become negative based on the past 24 hours usage and current balance. If it’s less than 5 days, the system will send a balance alert to your Tencent Cloud account creator and all collaborators via email, and SMS.



### Arrears alert

For pay-as-you-go resources, fees are deducted on the hour. When your account balance becomes negative, we will notify the Tencent Cloud account creator and all collaborators via email and SMS.



### Arrears processing

**Starting from the moment your account balance becomes negative:**

- You can continue to use your database for 24 hours from the moment your account balance becomes negative. We will continue to bill you for this period.
- When your account has been in arrears for 24 hours, **your database instances will automatically shut down, and we will stop billing you for this service**.

**After automatic shutdown:**

- Within 3 days of automatic shutdown, if your account is not brought up to a positive balance, you will not be able to start up your database; if your balance is positive, billing continues, and you can start up your database.
- If your account balance remains negative for 3 days after shutdown, the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all collaborators via email and SMS when the database is repossessed.

> **Note:**
>
> After you stop using pay-as-you-go resources, **terminate them as soon as possible** to avoid further fee incursion.
> Since your actual resource consumption is constantly changing, some slight discrepancies may exist for your stated balance.



## 1. Monthly Subscription TencentDB Instances Arrears

### Expiration alert

Seven days before the expiration of your monthly subscription, we will begin sending a reminder to the Tencent Cloud account creator and all collaborators every other day via email and SMS.

 

### Arrears alert

On the day when your monthly subscription expires and every two days after that, we will send an arrears isolation reminder to the Tencent Cloud account creator and all collaborators via email and SMS.

 

### What happens when your monthly subscription expires?

- Seven days before the expiration of your cloud services, the system will send you a renewal notification. 
- You can continue using your cloud services for an additional period of seven days after expiration. The system will send you an expiration reminder, and you should renew them as soon as possible.
- From the eighth day after expiration, you will not be able to use your database, which will be put into the **recycle bin**. You can view and renew your database resources on the recycle bin page on the console.
- Resources in the recycle bin will be retained for **seven days**. If the database in the recycle bin is not renewed within 7 days, it will be repossessed, and all data will be deleted and cannot be recovered. 
- In other words, there is a **7-day usable period** and a **7-day unusable period** for an expired database. Within the 14 days, you can opt to renew at any time. If your balance is sufficient and auto-renewal is enabled, your resources will be automatically renewed upon expiration.