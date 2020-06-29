Tencent Cloud offers two ways to purchase a CVM instance: pay as you go and spot instances. Each is suited to meet different customer needs.
The following table compares the two billing plans:

| Instance billing plan  | Pay as you go | Spot instances |
|---------|:---------:|:---------:|
| Payment method  | Deposit upon purchase. Billed by the hour. | Deposit upon purchase. Billed by the hour. |
| Payment unit  | USD/sec | USD/sec |
| Unit price | Pricy | The price fluctuates. In most cases, the price is about 10-20% of the price of a pay-as-you-go instance with the same specifications. |
| Minimal use time | Charged by the second and billed by the hour. Purchase and release at any time. | Charged by the second and billed by the hour. Purchase and release at any time. May be repossessed by the system. |
| Changing instance configurations | No limit. Change at anytime. | Not supported. |
| Use cases | Best for use cases such as an e-commerce flash sale where the demand for resources can fluctuate drastically in a short amount of time. | Best for use cases such as online and website services that use big data computing and load balancing. |


### Pay as you go

Pay as you go is a flexible billing plan for CVM instances. You can activate and terminate a CVM instance at any time and will be billed for what you use. You pay **by the second** and no up-front payment is required. A bill is generated every hour on the dot. This billing plan is suitable for use cases such as an e-commerce flash sale where the demand for resources can fluctuate drastically in a short amount of time.

When you purchase a pay-as-you-go CVM instance, an hour’s charge (including charges for the CPU, the memory, and the data disks) will be deducted from your account and frozen as a deposit. You will then be billed by the hour (Beijing time) for your usage over the past hour. When you purchase a CVM instance, the price will be listed as an hourly charge. However, you will actually be **billed by the second** and the charge will be rounded to the nearest two decimal places. Billing starts from the second the instance is created and stops the second the instance is terminated.

When a pay-as-you-go CVM instance is created, an hour’s charge will be deducted from your account and frozen as a deposit. When you adjust the CVM configurations, the current deposit will be released and a new deposit will be deducted based on the price of the new CVM instance. Your deposit will be released back to your account when the CVM instance is terminated.

Eligible pay-as-you-go instances (CPU and memory) will not be charged after shutdown. For more information, refer to [Details of No Charges When Shut Down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19918). Ineligible instances will still be charged after shutdown.

## Spot Instances

Spot instance is a new way to use and pay for CVM instances. Similar to pay as you go, you are charged by the second and billed by the hour for spot instances. The prices of spot instances fluctuate according to market demand. You will usually get a substantial discount for them (about 80-90% off the prices of pay-as-you-go instances with the same specifications). However, spot instances may be repossessed automatically by the system as a result of inventory shortages or higher bids from other users.
- For more information on spot instance policies, use cases, and limitations, refer to [Spot Instances](https://intl.cloud.tencent.com/document/product/213/17816).

