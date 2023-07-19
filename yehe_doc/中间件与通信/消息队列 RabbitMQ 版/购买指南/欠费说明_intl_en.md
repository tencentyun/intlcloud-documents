>! If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

This document describes the overdue payment policy for **monthly subscribed** exclusive clusters.

## Notes

- When you no longer use clusters, terminate them as soon as possible to avoid further fee deductions.
- After clusters are terminated/repossessed, their data will be deleted and cannot be recovered.

  

## Expiration alert

Seven days before your monthly subscribed cluster expires, the system automatically pushes an expiration alert message to you every other day. All alert messages are sent to the Tencent Cloud account creator and all collaborators by **email and SMS**.

## Overdue payment reminder

From the day when your monthly subscribed cluster expires, the system pushes an alert message of resource isolation due to overdue payment to you every other day. All alert messages are sent to the Tencent Cloud account creator and all collaborators by **email and SMS**.

## Overdue payment policy

If your account balance is sufficient and you previously enabled auto-renewal, the resource will be automatically renewed on the expiration date.

Your cluster can be used normally within 7 days after expiration. If you renew it during this period, **the billing cycle of the renewed cluster will start from the expiration date of the previous cycle**.

If your cluster is not renewed within 7 days after expiration, it will be suspended. Then, the system will process it as follows:

| Time After Service Suspension | Description                                                         |
| ---------------- | ------------------------------------------------------------ |
| ≤ 7 days | After the service is suspended, the console and APIs cannot be used. The cluster metadata will be retained. During this period, if you renew the cluster, it will be resumed. |
| > 7 days | If you don't renew your cluster within 7 days after suspension, your cluster resources will be terminated. All data will be deleted and cannot be recovered. When your resources are terminated, your Tencent Cloud account creator and all collaborators will be notified by email and SMS. |

> !
>
> - Once you receive an overdue payment reminder, top up your account in the [console](https://console.cloud.tencent.com/account/recharge) as soon as possible to prevent your business from being affected.
> - If you have any questions about bills, check your bill details on the [Resource Bills](https://console.cloud.tencent.com/account/resources) page in the console.
> - If you have any questions about fees, see [Purchase Guide](https://www.tencentcloud.com/document/product/1112/43067) for the description of each billable item and billing rules.
> - You can also configure alarms for overdue payments through the balance alert feature in the Billing Center. For more information, see [Balance Alerts](https://intl.cloud.tencent.com/document/product/555/9942).

