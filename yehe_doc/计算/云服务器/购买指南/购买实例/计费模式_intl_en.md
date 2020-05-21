Tencent Cloud offers two ways to purchase a CVM instance: pay as you go, or spot instances. They are each suited for different use cases.
The following table compares the two billing plans:

| Instance billing plan  | Pay-as-you-go | Spot instances |
|---------|:---------:|:---------:|
| Payment method  | [Deposit upon purchase](https://intl.cloud.tencent.com/document/product/555/12039). Billed on the hour. | [Deposit upon purchase](https://intl.cloud.tencent.com/document/product/555/12039). Charged by the hour. |
| Payment unit  | USD/Sec | USD/Sec |
| Unit price | Pricier | Price fluctuates. In most cases the price is about 10% - 20% of the price of a pay-as-you-go instance with the same specifications. |
| Minimal use time | Charged by the second and billed on the hour. Purchase and release at any time. | Charged by the second and billed on the hour. Purchase and release at any time. May be repossessed by the system. |
| Instance specification change | No limit. Change at anytime. | Not supported. |
| Use cases | Best for use cases where resource requirements vary drastically, such as e-commerce. | Best for scenarios such as online and website services with big data computing and load balancing. |



### Pay as you go

Pay as you go is a flexible billing plan for CVM instances. You can activate and terminate a CVM instance at any time and are billed for what you use. You pay **by the second** and no up-front payment is required. A bill is generated every hour on the dot. This billing plan is suitable for use cases such as an e-commerce flash sale where the demand for resources can fluctuate drastically.

When you purchase a pay-as-you-go CVM instance, an hour’s charge (including charges for CPU, memory and data disks) is deducted from your account and frozen as a deposit. You are then billed on the hour (Beijing time) for your usage over the past hour. When you purchase a CVM instance, the price is listed as an hourly charge. You are actually **billed by the second** and the charge is rounded to the nearest two decimal places. Billing starts from the second the instance is created and stops on the second the instance is terminated.

When a pay-as-you-go CVM instance is created, one hour of the CVM’s charge is deducted from your account and frozen as a deposit. If you adjust the CVM specification, the current deposit is released and a new deposit is deducted based on the price of the new CVM instance. Your deposit is released back to your account when the CVM instance is terminated.

Eligible pay-as-you-go instances (CPU and memory) are not charged after shutdown. For details, refer to [Details of No Charges When Pay-as-You-Go Instances Shut Down](https://intl.cloud.tencent.com/document/product/213/19918). Ineligible instances are still charged after shutdown.

## Spot Instances

Spot Instance is a new way to use and pay for CVM instances. Similar to pay as you go, you pay for spot instances by the second, on the hour. The price of spot instances fluctuates according to market demand. You usually get a sizable discount for them (about 80 to 90% off the price of pay-as-you-go instances with the same specifications). However, they may be repossessed automatically by the system as a result of inventory shortages or bidding from other users.
- For more information on spot instance policies, use cases and limitations, refer to [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816).

