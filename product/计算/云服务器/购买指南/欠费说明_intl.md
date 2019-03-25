## Pay-as-you-go CVM Expiration Reminder
### Arrears Reminder
Fees for pay-as-you-go resources are deducted on the hour. Email and SMS notifications will be sent to the Tencent Cloud account creator and all collaborators if your account balance falls below 0.

### Arrears Processing
When your balance falls below zero, you can continue to use CVM for the next **2** hours. We will also continue to bill you for this usage.
After 2 hours, if your account is not topped up to a positive balance, CVM service and billing will automatically be stopped. 

**After automatic shutdown:**
- Within 24 hours after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your CVM; If your balance is positive, the billing continues, and you can start your CVM. 
- If your account remains negative for 24 hours after shutdown, your pay-as-you-go CVM will be repossessed, and all data will be deleted and cannot be recovered.
We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when your CVM is repossessed.

> **Notes:** 
>- When you no longer use pay-as-you-go resources, **terminate them as soon as possible** to avoid further fee deduction.
>- After the CVM is terminated or repossessed, the data will be deleted and cannot be recovered.
>- Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.

## Network Billed by Traffic
### Balance Reminder
Network traffic consumption tend to fluctuate significantly and is difficult to predict. Therefore, we do not offer balance reminders.

### Arrears Reminder
When your balance falls below zero, you can continue to use the network billed by traffic for the next **2** hours. We will also continue to bill you for this usage. After 2 hours, if your account is not topped up to a positive balance, the network service billed by traffic will automatically be stopped. 

After the balance is topped up to positive, the service will resume. Please check the network settings and resume the binding of the affected CVM and load balancers.

