## Reminders and Alerts
### Pay-as-you-go amount overdue reminder

![](https://main.qcloudimg.com/raw/2b456d2454d45297292f63d2551c3951.png)

### Balance alert
On a daily basis, we estimate your pay-as-you-go account's remaining available working time based on your balance and usage during the past 24 hours. We will send you a balance alert if the remaining time is less than 5 days. Alert will be sent to Tencent Cloud account creator as well as all collaborators via email, SMS and call.


### Arrears alert
Fees are deducted every hour on the hour for pay-as-you-go method. We will notify the Tencent Cloud account creator and all collaborators via email and SMS if  your balance falls below zero.


### Arrears processing
The CFS file system can be used normally within 24 hours after your account falls into arrears (the orange segment in the above figure), but there will be a prompt of suspense of the service on the console.

Within 24-168 hours(7 days) after the arrears (the red segment in the above figure), if your account balance is not topped up to an amount greater than 0, the CFS service will be suspended and the billing will be stopped. The file system cannot be read or written, and the console only supports top-up operations. When the balance is topped up to an amount greater than 0, the billing will continue and the file system can be read and written.

If your negative balance lasts for 7 days (the black segment in the above figure), the postpaid CFS file system will be reclaimed, and all data will be cleared and cannot be recovered.

Tencent Cloud account creator and all the collaborators will be notified of the reclaim via email and SMS.

Note:
	•	Terminate pay-as-you-go service as soon as possible after you stop using it to avoid future fee deduction.
	•	After termination or reclaim, data will be erased and cannot be restored.
	•	Because your actual usage fluctuates, the balance alert may not be accuate.



