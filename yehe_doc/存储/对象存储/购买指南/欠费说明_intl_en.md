If your account has overdue payment, a notification will be sent to you. Once receiving it, please go to the [Billing Center](https://console.cloud.tencent.com/account/recharge) in the console and pay the past due charges in time to prevent your business from being affected. This document will provide detailed information on overdue payment.

## Causes

You can learn about why overdue payment happens by browsing FAQs as below:

- [Why does my account have overdue payment or incur charges even if I am eligible for the free tier?](https://intl.cloud.tencent.com/document/product/436/10373)



>?
>- If you have any question, please check [Bill Overview](https://console.cloud.tencent.com/expense/bill/overview) in the console. For more information, please see [Viewing Billing Details](https://intl.cloud.tencent.com/document/product/436/31631).
>- See [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776) for the description of each billing item and billing rules.
>- For information on the billing cycle of each billing item, see [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871).


## Service Status in the Case of Overdue Payment


1. COS service is still available within 24 hours after your account has overdue payment, with a service suspension notification sent to you in the console. In this case, please pay charges so that your account balance is not less than 0 in order to avoid affecting your business.
2. COS service will be automatically suspended after 24 hours with overdue payment. You cannot read or write any data in COS, while charges will still accrue for the **storage usage of your data** until it is destroyed. Before the destruction, COS will retain your data for 120 days considering its potential importance. During this period, all you can do using the console is pay charges. Ensure that your account balance is not less than 0 so that the service can be activated again.
3. After 120 days on end with overdue payment, you will be deemed to have waived the COS service. With no promise to further retain your data, it will be destroyed and cannot be recovered.


## How to Avoid or Process Overdue Payment


1. You can choose to delete COS data which you find useless to avoid any further charges.
2. You can enable **Monthly Expense Alert** in **Console** > **Billing Center** to receive notifications when your available balance falls below the alert threshold.
3. In case of overdue payment, please pay charges timely so that your account balance is not less than 0.
