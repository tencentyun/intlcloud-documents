## Package Balance Reminder

When the available balance of a package is lower than the set threshold, the system will send alarm notifications to the configured alarm contacts. In order to ensure the normal operation of your business, please enable auto-renewal for the package or purchase new packages in time. When the number of remaining messages in the package is less than the number of messages to be sent, the sending will fail. You need to purchase a sufficient package before you can continue to use the service.
You can set the package balance reminder in [Package Management](https://console.cloud.tencent.com/smsv2/manage-package) based on your actual business needs. For detailed directions, please see [Package Settings](https://intl.cloud.tencent.com/document/product/382/35466).

## Package Expiration Reminder
The system will send expiration reminders one every other day starting 7 days before the package expires (i.e., on days 7, 5, 3, and 1 before the expiration) to your Tencent Cloud creator through email, SMS, and internal message.

## Repossession Mechanism

- The system will send expiration reminders starting 7 days before the package expires.
- If your account balance is sufficient and you have configured [auto-renewal](https://intl.cloud.tencent.com/document/product/382/35451), the renewed messages will take effect as a new package, which will be valid for 2 years from the date of successful renewal.
- After the package expires, its status will become **expired** and any remaining balance of it will become unavailable.
