### Are cloud disks billed independently?
Elastic cloud disks are billed independently based on a pay-as-you-go basis.

### How are cloud disks priced?
The billing mode for cloud disks is pay-as-you-go. Pricing varies by cloud disk types and billing modes. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
### How much is the pay-as-you-go cloud disk?
Billing standard for different types of pay-as-you-go cloud disks varies by regions. For more information, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

### How will users be notified when pay-as-you-go CBS data disks expire?
The system estimates the number of days it takes your account balance to become negative based on the current balance and your usage in the past 24 hours. If it is less than 5 days, the system will send a balance alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, the Message Center, etc.

### How will users be notified when pay-as-you-go CBS data disks are in arrears?
Pay-as-you-go resources are billed on the hour. When your account becomes negative, the system will send a balance alert to your Tencent Cloud account creator and all collaborators who have subscribed to messages via email, SMS, the Message Center, etc.

### What is the repossession mechanism for pay-as-you-go CBS data disks?
- You can continue to use the pay-as-you-go cloud disk for 2 hours from the moment your account becomes negative. You will be billed for this period. After 2 hours, the service will automatically shut down (cloud disk is unavailable and only data is retained) and billing stops.
- If your Tencent Cloud account is topped up to a positive balance within 24 hours after the automatic shutdown, the cloud disk will be restored and billing continues.
- If the balance is less than 0 for 24 hours after the cloud disk has service suspended, the system will repossess the pay-as-you-go disk. All data will be erased and **cannot be retrieved**. Tencent Cloud account creator and all collaborators will be notified via email, SMS, the Message Center, etc.

