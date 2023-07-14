>!
If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

## Overdue Payments and Service Suspension
Lighthouse instance packages are prepaid. Generally, if your account has overdue payments, instance usage will not be affected. However, if your account and instances meet the following conditions at the same time, your instances will be suspended due to overdue payments and displayed as in **to be repossessed** status in the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
- Condition 1: the account has overdue payments.
- Condition 2: the instances use traffic packages, and the current monthly traffic usage has exceeded the package limit.

## Impact of Overdue Payments
### Impact on instance
Instances in **to be repossessed** status are unavailable, which indicates that they can neither be managed nor accessed.

### Impact on custom image
- The custom image feature will be disabled, and you cannot create more custom images.
- All custom images (including those within the free tier) under your account will enter the **to be repossessed** status. If you don't top up your account within seven days, the custom images will be automatically released.

## Recovery Method
 - Recover an account in arrears: you can top up or use other methods to make your account balance positive, and then all instances in **to be repossessed** status will be automatically recovered.
 - Recover an instance with excessive traffic usage: an instance that is purchased for multiple months can become available from the **to be repossessed** status after its monthly [traffic package](https://intl.cloud.tencent.com/document/product/1103/41403) is reset. If the instance generates excessive traffic again, it will enter the **to be repossessed** status again.

## Alert Description
<table>
    <tbody><tr><th>Alert Type</th><th>Description</th></tr>
    <tr><td><b>Alert for expiration</b></td><td>From seven days before your resource expires, the system will send alerts for expiration to your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS.</td></tr>
    <tr><td><b>Alert for overdue payments</b></td><td>On the day of and after resource expiration, the system will send alerts for service suspension to your Tencent Cloud account creator and all collaborators by email and SMS.</td></tr>
</tbody></table>

## Repossession Mechanism
- From seven days before your resource expires, the system will send you renewal notifications.
- If your account balance is sufficient and you previously enabled auto-renewal, the instance will be automatically renewed on the expiration date.
- If your Lighthouse instance is not renewed before or upon expiration, the system will suspend it in around 48 hours after expiration (the instance will be disconnected and shut down, and only the data will be retained). After suspension, the instance will enter the **to be repossessed** status.
- You can still renew the instance within seven days after suspension.
>!The start time of the renewal cycle of an instance that is recovered after renewal is the time of the last suspension.
>
- If your Lighthouse instance is not renewed within seven (included) days after entering the **to be repossessed** status, the system will release it in around 24 hours. After release, all data on the instance will be cleared and cannot be recovered.





