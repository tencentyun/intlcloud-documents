## Monthly subscription cloud disks

### Expiration Alerts

Starting 7 days before your monthly subscription resources expire, we will send you an expiration alert every other day (i.e., on the 7th, 5th, 3rd, and 1st days before expiration). The account creator will be notified via email, SMS, and the Message Center. All collaborators under the account can configure the receipt method in the console -> Message Center -> [Message Subscription](https://console.cloud.tencent.com/message/subscription) and add recipients.

### Overdue Payment Alerts

On the day your monthly subscription resources expire (the 1st day of the expiration) and every other day thereafter (the 3rd, 5th, 7th days, etc.), we will send you an overdue payment alert. You can configure the receipt method in the console -> Message Center -> [Message Subscription](https://console.cloud.tencent.com/message/subscription) and add recipients.

### Repossession Mechanism

- 7 days before the resources expire, you will receive an expiration alert and a renewal reminder.
- If your account balance is sufficient and auto renewal is enabled, cloud disk will automatically renew on the expiry date.
- If your cloud disk is not renewed before expiration (including on the expiry date), it can still be used for 7 days after the expiry date. If your cloud disk is not renewed within 7 days after it expires, it will be **forcibly unmounted** from a CVM (if any) and its services will be suspended (the cloud disk is unavailable and can only store data). The disk will enter the recycle bin, where you can still restore and renew it. However, **the billing cycle of the renewed cloud disk starts on the end date of the previous billing cycle**.
- If your cloud disk is not renewed within 7 days after it enters the recycle bin, resources will be released and data in the expired cloud disk will be erased and **cannot be recovered**.

## Pay-as-you-go cloud disks
>!
>- For pay-as-you-go resources no longer used, **terminate them as soon as possible** to avoid fee deduction.
>- Because your actual resource consumption changes constantly, the timing of a balance alert may deviate.

![](https://main.qcloudimg.com/raw/becc841c9f150f7ad781da71278fbed3.png)

### Balance Alert
The system estimates the number of days it takes for your account balance to become negative based on the current balance and your usage in the past 24 hours. If it is less than 5 days, the system will send a balance alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, and the Message Center.

### Overdue Payment Alerts
Pay-as-you-go resources are billed by the hour. When your account balance becomes negative (Point 1 in the figure above), the system will send an alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, and the Message Center.

### Overdue Payment Processing

- You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account balance becomes negative. You will be billed for this period. After 2 hours (Point 2 in the figure above), its services will be suspended (cloud disk is unavailable and can only store data). You will still be billed according to the billing standard (even if the account balance is negative) until data is completely erased.
- If your Tencent Cloud account is topped up to a positive balance within 15 days after the cloud disk has its services suspended, the disk can be restored.
- If the balance is less than 0 for 15 days after the cloud disk has its services suspended (Point 3 in the figure above), the pay-as-you-go disk will be repossessed. All data will be erased and **cannot be recovered**. Tencent Cloud account creator and all collaborators will be notified via email, SMS, and the Message Center.
