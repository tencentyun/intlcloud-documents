## Monthly Prepaid

### Expiration Alert

Within seven days before expiration, the system will push expiration alerts.

### Expiration Handling
1. Within 24 hours after expiration, the system automatically renews the account if auto-renewal is enabled and the account balance is sufficient.
2. More than 24 hours after expiration, the cross-region bandwidth drops to 10 kbit/s if the account is not renewed.
![](https://main.qcloudimg.com/raw/49be4e1ed5ff3b5695a9f40557e6a106.png)

## Monhtly Postpaid (bill by 95th Percentile)
### Arrears Alert
1. Arrears notification: The system pushes an arrears notification when the account balance becomes negative.
2. Arrears alert: This feature is disabled by default. To enable this feature, see [Balance Alert Guide](https://cloud.tencent.com/document/product/555/9942) to subscribe to this feature.

### Arrears Processing
The system handles arrears based on the time starting from the moment when the balance drops to 0. The logic is as follows:
1. Within seven days, Cloud Connect Network (CCN) is still available for the account.
2. Seven days later, the CCN becomes unavailable and the cross-region bandwidth drops to 0 kbit/s if your account balance is still negative. However, the configurations of the CCN are retained and the CCN becomes available after you recharge your account.
![](https://main.qcloudimg.com/raw/f98537d47bd8dc290ba75db851f45ef1.png)

>All operations and status changes are pushed to the creator of a Tencent Cloud account, the global resource collaborator, and the financial collaborator via emails and SMSs.
