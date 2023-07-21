>!If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

## Arrears Reminder for Pay-as-you-go Resources
![](https://main.qcloudimg.com/raw/23ef4b0d1cc37f6d73627978ffd79e83.jpg)

## Alert for Insufficient Balance
We will estimate the number of days it takes your account balance to become negative based on the usage in the last 24 hours and current balance. If it is less than 5 days, we will send a reminder to your Tencent Cloud root account and all the subaccounts via email, SMS, and phone call.


## Alert for Arrears
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is below zero, we will notify your Tencent Cloud root account and all the subaccounts via email,SMS,and Message Center.


## Arrears Processing
1. The CFS file system can be used normally within 24 hours after your account falls into arrears (as shown in the orange segment in the figure above), but there will be an alert informing you of upcoming service suspension in the console.
2. If your account is not topped up to a positive value between 24 hours and 168 hours (as shown in the red segment in the figure above) after your account falls into arrears, CFS will suspend the service, the file system will not be available for reads/writes but will still be billed, and only the top-up operation can be performed in the console. After your account balance becomes positive, the service will be automatically resumed and available for reads/writes.
3. If your account balance remains negative for 7 days (as shown in the black segment in the figure above), the pay-as-you-go CFS file system will be repossessed. At this point, all data will be cleared and cannot be recovered.
4. Your Tencent Cloud root account and all the subaccounts will be notified of the CFS repossession via email,SMS,and Message Center.

>!
>- When you no longer need to use pay-as-you-go resources, please terminate them as soon as possible to avoid further fee deductions.
>- After a resource is terminated or repossessed, the data will be cleared and cannot be recovered.
>- As your actual resource consumption may change over time, there may be some deviation in the balance alert.
