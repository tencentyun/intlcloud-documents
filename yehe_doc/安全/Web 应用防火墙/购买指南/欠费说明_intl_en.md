>! If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

This document describes the payment overdue policy and data repossession mechanism of WAF, a monthly subscribed product.
## Expiration Alert
From **seven days before the expiration** of your WAF resource until it is released, the system will send an alert to your Tencent Cloud account creator, global resource collaborators, and financial collaborators via email, SMS, WeChat, and Message Center as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).

For more information on the alert mechanism from **seven days before the expiration** of your resource until it is released, see [Prepaid Billing](https://intl.cloud.tencent.com/document/product/555/42701).

## Overdue Payment Reminder
On and after the **day of expiration** of your WAF instance resource, the system will send alerts for resource isolation to your Tencent Cloud account creator and all collaborators via email, SMS, WeChat, and Message Center as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message).

## Repossession
- The system will send you a renewal notification **seven days before the expiration** of your WAF resource.
- You can continue using WAF for **an additional seven days after the expiration**. The system will send you an expiration reminder, and you need to renew it as soon as possible.
- WAF will be suspended **eight days after the expiration**. The forwarding and protection features will become unavailable, but configuration data will be retained, and you still can renew it in the console. After WAF is suspended:
    - **DNS resolution will not be adjusted**. If you are sure that you will no longer use WAF, resolve your domain names to the real serer; otherwise, website services will be inaccessible.
    - **Domain names and CLB listeners will not be unbound**, and you need to unbind them before resources are repossessed.
- If you don't renew WAF within **14 days after the expiration**, resources will be repossessed by the system, and data will be cleared and cannot be recovered. In other words, there is a **seven-day usable period** and a **seven-day unusable period** for an expired WAF resource. Within the 14 days, you can opt to renew at any time. If your balance is sufficient and auto-renewal is enabled, your resources will be automatically renewed upon expiration.

>!
>- If your account balance is sufficient and you previously enabled auto-renewal, the system will perform renewal automatically on the expiration date.
>- If you account balance is insufficient for the renewal, the system will send you the notification "Your account balance is insufficient for the renewal and you need to top up your account" via email, SMS, WeChat, and Message Center as configured in the message subscription in the [Message Center](https://console.cloud.tencent.com/message). You will receive one notification every other day and receive a phone call one day before the expiration.

## Releasing Instance Resource
After your WAF resources expire, you can release them in the console.
![](https://qcloudimg.tencent-cloud.cn/raw/f0ad4cd02213a218b3e5c047949d2577.png)

1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-overview) and select **Instance management** on the left sidebar.
2. On the **Instance management** page, select the target instance and click **Release instance**.
3. After the instance is released, the backend will **clear all its configurations**. If you still want to use it, cancel the operation and renew the instance as soon as possible.
