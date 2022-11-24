## Monthly Subscription
### Expiration alert
From seven days before your monthly subscribed resource expires, the system will send alerts for expiration to your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS.

### Overdue payment alert
Pay-as-you-go resources are billed on every clock-hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email and SMS.

### Repossession
- From seven days before your monthly subscribed data engine expires, the system will send you renewal notifications.
- If your account balance is sufficient and you have previously enabled automatic renewal, the system will renew your data engine automatically on the day it expires. If your account balance is insufficient, the renewal will fail.
- If you fail to renew your data engine before its expiration time, it will expire, and the system will automatically send expiration notifications.
- After the data engine expires, **the system will isolate it in 24 hours.** It will become unavailable, with the data retained though.
- You can renew the isolated data engine on the **Data engine** page in the **Data Lake Compute console** to recover it.
>! The billing cycle of a data engine that is renewed from the isolated status will start from the expiration date of the previous cycle.
- **You cannot return the data engine again within six hours after you renew and recover it from isolation.**
- The isolation period is seven days. If you don't renew the data engine before the isolation period elapses, the system will terminate the data engine permanently.
- The system will notify your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS when your data engine is terminated.


## Pay-as-You-Go
### Overdue payment alert
Pay-as-you-go resources are billed on every clock-hour. When your account balance becomes negative, your Tencent Cloud account creator, global resource collaborators, and financial collaborators will be notified by email and SMS.
### Processing for overdue payments
#### Public engine
From the time point when **your account balance becomes negative**, you cannot use the public engine for data computing.
#### Pay-as-you-go private engine
Within **one hour** after your account balance becomes negative, your private engine will still be available and incur fees. After one hour, it will be isolated and stop incurring fees. It then cannot be used for data computing.

After the data engine is isolated:
- Within **seven days (7 * 24 hours)** after your data engine is isolated, if you top up your account to a positive balance, it will be recovered from isolation and continue to incur fees, and you can use it for data computing. If your account balance remains negative, it will remain isolated.
- If your account **still has overdue payments** for **seven days (7 * 24 hours)** after your pay-as-you-go data engine is isolated, after the isolation period elapses, **it will be terminated permanently.**

The system will notify your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS when your data engine is terminated.