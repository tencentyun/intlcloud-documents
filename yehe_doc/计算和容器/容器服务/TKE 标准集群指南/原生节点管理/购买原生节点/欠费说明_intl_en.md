If your account has overdue payment, a notification will be sent to you. Once receiving it, please go to the [Billing Center](https://console.cloud.tencent.com/account/recharge) in the console and pay the past due charges in time to prevent your business from being affected. This document will provide detailed information on overdue payment of native nodes.





## Alerting

| Reminder Type | Description |
| ------------ | ------------------------------------------------------------ |
| **Expiration** | Seven days before cluster resource expiration, the system will send an expiration alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS. |
| **Overdue payment** | On the day of and after cluster resource expiration, the system will send an overdue payment alert to your Tencent Cloud account creator and all collaborators by email and SMS. |


## Repossession


>?
>- Suspension: When the resource of a user is suspended, the user cannot use the resource any more. However, data of the resource is not deleted, and the user can resume the resource.
>- Release: Data of a resource is deleted, and the resource cannot be resumed.

### Pay-as-you-go instance repossession mechanism
- Starting from the point when your account balance becomes negative, the native node instances are still available for the next **two hours**, and the billing continues. Two hours later, if your account is still not topped up to a balance greater than zero, the native node instances will be suspended and released (the node resources will be terminated, and data cannot be restored).
- If your account is topped up to a balance greater than zero two hours after your account has overdue payments, the fees of the native node instances will be calculated and deducted according to the pay-as-you-go billing rules.
