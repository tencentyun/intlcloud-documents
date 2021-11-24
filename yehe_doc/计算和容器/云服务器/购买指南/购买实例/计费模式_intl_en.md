Tencent Cloud offers two ways to purchase a CVM instance: pay as you go and spot instance. Each is suited to meet different customer needs.
The following table compares the two billing plans:

| Instance billing plan  | Pay as you go | Spot instance |
|---------|:---------:|:---------:|
| Payment method  | [Deposit](https://intl.cloud.tencent.com/document/product/555/12039) upon purchase, billed hourly | [Deposit](https://intl.cloud.tencent.com/document/product/555/12039) upon purchase, billed hourly |
| Payment unit  | USD/sec | USD/sec |
| Unit price | Relatively higher | The price fluctuates. In most cases, the price is about 10-20% of the price of a pay-as-you-go instance with the same specifications. |
| Minimal use time | Charged by the second and billed by the hour. Purchase and release at any time. | Charged by the second and billed by the hour. Purchase and release at any time. May be repossessed by the system. |
| Changing instance configurations | No limit. Change at anytime. | Not supported. |
| Use cases | Best for use cases where the business demand fluctuates greatly, such as ecommerce flash sales. | Best for use cases such as online and website services that use big data computing and load balancing. |


## Pay As You Go

Pay as you go is a flexible billing plan for CVM instances. You can activate and terminate a CVM instance at any time. You only need to pay for what you use accurate down to **second** with no upfront payment required. Pay-as-you-go resources will be billed on the hour. This billing plan is suitable for use cases where the business demand fluctuates greatly, such as ecommerce flash sales.

When you activate a pay-as-you-go CVM instance, an hour’s charge (including charges for the CPU, the memory, and the data disks) will be frozen in your account balance as a deposit. You will then be billed by the hour (Beijing time) for your usage over the past hour. When you purchase a CVM instance, the price will be listed as an hourly fee. However, you will actually be **billed by the second** and the charge will be rounded to the nearest two decimal places. Billing starts from the second the instance is created and stops the second the instance is terminated.

When a pay-as-you-go CVM instance is created, an hour’s charge will be frozen in your account balance as a deposit. When you change the CVM configurations, the current deposit will be released and a new deposit will be frozen based on the unit price of the new configuration. Your deposit will be released back to your account when the CVM instance is terminated.

You can enable No Charges When Shut Down for pay-as-you-go instances to stop the billing of CPU and memory fees after the instance is shut down. For limitations on this feature, refer to [No Charges When Shut Down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19918). 

## Spot Instance

Spot instance is a new way to use and pay for CVM instances. Similar to pay as you go, it allows you to be charged by the second and billed by the hour. The prices of spot instances fluctuate according to market demand, which provide you with a substantial discount (about 80-90% off the prices of pay-as-you-go instances with the same specifications). However, spot instances may be repossessed automatically by the system as a result of inventory shortages or higher bids from other users.
- For more information on spot instance policies, use cases, and limitations, refer to [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816).

