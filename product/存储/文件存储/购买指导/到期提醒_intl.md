## Reminders and Alerts
### Pay-as-you-go Arrears Reminder

![](https://main.qcloudimg.com/raw/2b456d2454d45297292f63d2551c3951.png)

### Balance Reminder
We will estimate the number of days it takes your account balance to become negative based on the past 24 hours usage and current balance. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.


### Arrears alert
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative, we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.


### Arrears processing
You can continue to use the CFS file system for 24 hours from the moment your account becomes negative (the orange segment in the above figure). The console will display a reminder that service will soon be suspended.

After 24 hours, if your account is not topped up to a positive balance (the red segment in the above figure), CFS service will automatically be stopped. The file system cannot be read/written, and in the console you can only add funds. Your service will remain unavailable if your balance is not positive within 7 days after automatic shutdown. If your balance is positive, services and read/write will resume automatically.

If your balance remains negative more than 7 days after automatic shutdown (the black segment in the above figure), CFS file system will be repossessed, and all data will be deleted and cannot be recovered. Email and SMS notifications will be sent to the Tencent Cloud account creator and all collaborators 

> Note: 
	•	When you do not use pay-as-you-go resources any longer, **terminate them as soon as possible** to avoid further fee deduction.
	•	After the resource is terminated or repossessed, the data will be deleted and cannot be recovered.
	•	Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.




