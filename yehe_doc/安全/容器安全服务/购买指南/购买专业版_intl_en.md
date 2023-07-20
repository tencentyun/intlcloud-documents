This document describes the billing mode of TCSS Pro Edition and how to purchase it.
## Prerequisites
Before purchasing the TCSS Pro Edition, you need to [sign up for a Tencent Cloud account](https://www.tencentcloud.com/document/product/378/17985).

## Billing Overview
TCSS Pro Edition supports prepaid and postpaid billing modes.
- Prepaid: Monthly subscription is supported. Fees are charged by the number of CVM cores, each of which costs 6.75 USD/month (with discounts during promotion campaigns). The system will deduct fees at a time and generate a bill immediately.
- Postpaid: Billing by day is supported. Specifically, each core costs 0.25 USD/day.
>?
>- When the system detects that the total number of CVM cores in your business environment exceeds that of licensed cores of the Pro Edition, and you don't purchase more cores, fees will be deducted based on the average number of excessive cores of the day (excessive cores are counted once every hour) at 2:00 AM the next day.
>- You can configure the upper limit on the number of flexibly billed cores on the [TCSS purchase page](https://buy.cloud.tencent.com/tcss) based on the change in the number of cores in the business environment. Its minimum value is 500 cores/day.

## Purchase Methods
You can make a purchase in either of the following methods:
- Method 1: On the [TCSS purchase page](https://buy.cloud.tencent.com/tcss), select the desired number of cores and duration and click **Purchase now**.
- Method 2: Log in to the [TCSS console](https://console.cloud.tencent.com/tcss), click **Buy now** on the product guide page, select the desired number of cores and duration, and click **Purchase now**.

>?
>- When using TCSS Pro Edition, if the number of purchased virtual cores is fewer than the total number of cores on the container cluster node in the current business environment, the **Security Overview** page will prompt that your licensed cores are insufficient. To ensure your normal use of TCSS, purchase more cores as soon as possible.
>- If you don't purchase more cores, the flexible billing - postpaid mode will apply.
>- If you enable auto-renewal, the service will be renewed automatically monthly upon expiration if your account has a sufficient balance.

## Renewal
You can use the Pro Edition for additional five days after expiration. If you don't renew it within that period, the service will be suspended.

## Overdue Payments
#### Expiration alert
From seven days before your TCSS service expires, the system will send alerts for expiration to your Tencent Cloud account creator, global resource collaborators, and financial collaborators by email and SMS.
#### Overdue payment alert
On the day of and after TCSS service expiration, the system will send alerts for isolation to your Tencent Cloud account creator and all collaborators by email and SMS.
#### Repossession mechanism
- From seven days before your TCSS service expires, the system will send you renewal notifications.
- If your account balance is sufficient and auto-renewal is enabled, the service will be automatically renewed on the expiration date.
- You can still renew the service within five days after suspension on the **Activate service** page.
- If your TCSS service is not renewed within five days after expiration, the system will suspend it in around 24 hours after that period (the service will be suspended, and the data will be deleted).

>! If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

## Refund Policy
If you need fewer virtual cores in your business environment due to server deregistration, i.e., the number of cores of the Pro Edition exceeds the actual total number of cores, [contact us](https://intl.cloud.tencent.com/contact-us) for a refund application.
