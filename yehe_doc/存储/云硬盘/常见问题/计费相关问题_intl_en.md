### Are cloud disks billed independently?
Elastic cloud disks are billed independently. Monthly subscription and pay-as-you-go manner are supported.

### How are cloud disks priced?
CBS supports monthly subscriptions and pay-as-you-go manner. Pricing varies by cloud disk types and billing modes. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
### How much is the monthly subscribed cloud disk?
Pricing varies by region and disk type. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### How much is the pay-as-you-go cloud disk?
Pricing varies by region and disk type. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### How do I return the monthly subscribed CBS data disk?
To help you better use CBS services, we offer standard and 5-day free returns for monthly subscribed elastic cloud disks (i.e., data disks).
- Each verified individual or enterprise account can return **one** monthly subscribed elastic cloud disk within 5 (inclusive) days after purchase with no questions asked. The full refund will be returned to the Tencent Cloud account of the payer.
- Each account can return **199** monthly subscribed elastic cloud disks per year as standard returns. Fees for consumed resources will be deducted from the refund. The remaining amount, including **cash and free credits**, will be returned to the Tencent Cloud account of the payer.

For more information, see [Refunds](https://intl.cloud.tencent.com/document/product/362/36875).

### How are users notified about the expiration of monthly subscribed CBS data disks?
Starting 7 days before the expiration date of monthly subscribed resources, an expiration alert is sent every other day (i.e., on the 7th, 5th, 3rd, and 1st day before expiration). The account creator will be notified via email, SMS, and the Message Center. Collaborators can configure to receive this alert in the console > Message Center > [Message Subscription](https://console.cloud.tencent.com/message/subscription). For detailed directions, see [Balance Alert Guide](https://www.tencentcloud.com/zh/document/product/555/9942).

### How are users notified about the overdue payment of monthly subscribed CBS data disks?
On the day your monthly subscribed resources expire (the 1st day of the expiration) and every other day thereafter (the 3rd, 5th, 7th days, etc.), we will send you an overdue payment alert. You can configure the receipt method in the console -> Message Center -> [Message Subscription](https://console.cloud.tencent.com/message/subscription) and add recipients.

### What is the repossession mechanism for monthly subscribed CBS data disks?
The following instructions are only applicable to elastic cloud disks. The lifecycle of non-elastic cloud disks is the same as the associated CVMs. For more information, see [Payment Overdue](https://intl.cloud.tencent.com/document/product/213/2181).
- 7 days before the resources expiration date, you will receive an expiration alert and a renewal reminder.
- If your account balance is sufficient and auto-renewal is enabled, cloud disk will be auto-renewed on the expiry date.
- If your cloud disk is not renewed before it expires (including on the expiration date), the system will begin to limit its performance at the point in time of its expiration. When using the cloud disk, you will notice a significant decrease in performance.
- If your cloud disk is not renewed within 24 * 7 hours after it expires, the system will suspend its service processing (the cloud disk is unavailable, and can only store data), **force release** its relationship with the CVM (if any), and the cloud disk will be sent to the recycle bin. You can still retrieve the cloud disk from the recycle bin and renew it, but **the start time of the cloud disk that has been renewed and retrieved will be the previous period's expiration date**.
- If your cloud disk is not renewed within 24 * 7 hours after it's moved to the recycle bin, resources will be released and data in the expired cloud disk will be erased and **cannot be recovered**.

Call 4009100100 if you need further information.

### How are users notified about expiration of pay-as-you-go CBS data disks?
The system estimates the time that your account balance is about to run out based on the current balance and your usage in the past 24 hours. If the estimated time is within 5 days, an alert is sent to the Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, and the Message Center.

### How are users notified about overdue payment of pay-as-you-go CBS data disks?
Pay-as-you-go resources are billed and deducted on each clock hour. When your account becomes negative, the system will send an alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, the Message Center, etc.

### What is the repossession mechanism for pay-as-you-go CBS data disks?
- You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account balance becomes negative. You will be billed for this period. After 2 hours, the services will be suspended and cloud disk will only store data. Until data is completely deleted, you will still be billed according to the billing standard even if the account balance is negative.
- If your Tencent Cloud account is topped up to a positive balance within 15 days after the cloud disk has its services suspended, the disk can be restored.
- If the account balance remains negative for more than 15 days after the cloud disk services are suspended, the pay-as-you-go disk will be repossessed. All data will be erased and **cannot be recovered**. When your cloud disk is repossessed, the Tencent Cloud account creator and all collaborators will receive a notification via email, SMS, and the console Message Center.

Call 4009100100 if you need further information.
