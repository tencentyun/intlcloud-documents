## Reminders and Alerts
### Pay-as-you-go amount overdue reminder

![](https://main.qcloudimg.com/raw/2b456d2454d45297292f63d2551c3951.png)

### Balance alert
On a daily basis, we estimate your pay-as-you-go account's remaining available working time based on your balance and usage during the past 24 hours. We will send you a balance alert if the remaining time is less than 5 days. Alert will be sent to Tencent Cloud account creator as well as all collaborators via email, SMS and call.


### Arrears alert
Fees are deducted every hour on the hour for pay-as-you-go method. We will notify the Tencent Cloud account creator and all collaborators via email and SMS if  your balance falls below zero.


### Arrears processing
The CFS file system can be used within 24 hours after your account falls into arrears (the orange segment in the above figure). But on the console there will be a reminder that service will soon be suspended.

If you do not add funds and your balance is still below 0 within 24 to 168 hours (7 days) of the arrears (the red segment in the above figure), CFS service will be suspended. The file system cannot be read/written, and in the console you can only add funds. When the balance is above 0, services and read/write will resume automatically.

If your balance remain negative for 7 days (the black segment in the above figure), the postpaid CFS file system will be reclaimed, with all data deleted and unrecoverable.

Tencent Cloud account creator and all the collaborators will be notified of the reclaim via email and SMS.

Note:
	•	Terminate pay-as-you-go service as soon as possible after you stop using it to avoid future fee deduction.
	•	After termination or reclaim, data will be erased and cannot be restored.
	•	Because your actual usage fluctuates, the balance alert may not be accuate.



