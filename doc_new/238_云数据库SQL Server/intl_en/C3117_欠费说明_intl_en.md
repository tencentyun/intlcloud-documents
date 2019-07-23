## 1. Expiry Reminder for Prepaid TencentDB Instances
## 1.1. Alert for Expiry
We will start sending an expiration reminder every two days to your Tencent Cloud account creator and all the collaborators via email and SMS 7 days before prepaid resources expiration.

## 1.2. Alert for Arrears
On the day when prepaid resources expire and every two days after that, we will send an arrears isolation reminder to your Tencent Cloud account creator and all the collaborators via email and SMS.

### 1.3. Repossessing Mechanism
- The system will send you a renewal notification 7 days before the expiration of Tencent Cloud services resources.
- You can continue using the services for an additional period of seven days after the expiration. The system will send you an expiration reminder for the services, and you need to renew them as soon as possible.
- If you fail to renew the service resources within 7 days after the expiration date, the resources will be repossessed by the system and all the data will be cleared and cannot be recovered.

## 2. Arrears Reminder for Pay-as-you-go TencentDB Instances
![](https://main.qcloudimg.com/raw/3f29c0d5aefc7561d5d63e2940e8356f.png)
### 2.1. Balance Reminder
We will estimate the number of days it takes your account balance to become negative based on the past 24 hours usage and current balance. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.

## 2.2. Arrears Reminder
 For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative (Point 1 in the figure above), we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

### 2.3. Arrears Processing
You can continue to use the TencentDB instance for 2 hours from the moment your account becomes negative.
We will also continue to bill you for this period.
When your account is in arrears for 2 hours, (Point 2 in the figure above), the instance will be isolated and become inaccessible. We will also stop billing you for service.

Within 24 hours after automatic shutdown, 
if your account is not topped up to a positive balance, you will not be able to start your TencentDB instance; if your balance is positive, the billing continues, and you can start your instance. 
If your account remains negative for 24 hours after shutdown, (Point 3 in the figure above), the pay-as-you-go database will be repossessed, and all data will be deleted and cannot be recovered.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the database is repossessed.

>!
>- When you do not use pay-as-you-go resources any longer, terminate them as soon as possible to avoid further fee deduction.
>- After the database is terminated or repossessed, the data will be deleted and cannot be recovered.
>- Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.

