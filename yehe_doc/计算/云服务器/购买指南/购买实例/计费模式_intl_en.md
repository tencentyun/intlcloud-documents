Tencent Cloud offers three ways to purchase a CVM instance: pay-as-you-go , spot instance and reserved instance. Each is suited to meet different customer needs.
The following table lists the differences between the three billing modes:

| Instance Billing Mode  | Pay-as-You-Go | Spot Instance | Reserved Instance |
|---------|:---------:|:---------:|:---------:|
| Payment method  | [Amount freezing](https://intl.cloud.tencent.com/document/product/555/12039) upon purchase, billed hourly | [Amount freezing](https://intl.cloud.tencent.com/document/product/555/12039) upon purchase, billed hourly | Prepaid |
| Billing unit  | USD/second | USD/second | USD/year |
| Unit price | Relatively higher | The price fluctuates. In most cases, the price is about 10-20% of the price of a pay-as-you-go instance with the same specifications. | Relatively lower |
| Minimal use time | Charged by the second and billed by the hour. Purchase and release at any time. | Charged by the second and billed by the hour. Purchase and release at any time. May be repossessed by the system. | One year |
| Changing instance configurations | No limit. Change at any time. | Not supported. | Not supported. |
| Use case | Suitable for scenarios where the demand for devices fluctuates significantly in an instant, such as flash sale campaigns on an ecommerce site | Suitable for scenarios such as big data computing and online website service using load balancing | Suitable for businesses with stable and long-term device demands as a discount of pay-as-you-go instances with both high flexibility and cost performance |



## Pay-as-You-Go

Pay as you go is a flexible billing plan for CVM instances. You can activate and terminate a CVM instance at any time. You only need to pay for what you use accurate down to **second** with no upfront payment required. Pay-as-you-go resources will be billed on the hour. This billing plan is suitable for use cases where the business demand fluctuates greatly, such as ecommerce flash sales.

When you activate a pay-as-you-go CVM instance, an hour's charge (including charges for the CPU, the memory, and the data disks) will be frozen in your account balance as a deposit. You will then be billed by the hour (Beijing time) for your usage over the past hour. When you purchase a CVM instance, the price will be listed as an hourly fee. However, you will actually be **billed by the second** and the charge will be rounded to the nearest two decimal places. Billing starts from the second the instance is created and stops the second the instance is terminated.

When a pay-as-you-go CVM instance is created, an hour's charge will be frozen in your account balance as a deposit. When you change the CVM configurations, the current deposit will be released and a new deposit will be frozen based on the unit price of the new configuration. Your deposit will be released back to your account when the CVM instance is terminated.

Eligible pay-as-you-go instances (CPU and memory) will not be charged after shutdown. For more information about limitations, refer to [No Charges When Shut Down for Pay-as-You-Go Instances](https://intl.cloud.tencent.com/document/product/213/19918). Ineligible instances will still be charged after shutdown.

## Spot Instance

Spot instance is a new way to use and pay for CVM instances. Similar to pay as you go, it allows you to be charged by the second and billed by the hour. The prices of spot instances fluctuate according to market demand, which provide you with a substantial discount (about 80-90% off the prices of pay-as-you-go instances with the same specifications). However, spot instances may be repossessed automatically by the system as a result of inventory shortages or higher bids from other users.
For more information on spot instance policies, use cases, and limitations, see [Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816).

## Reserved Instance

The reserved instance (RI) billing mode is a more favorable prepaid billing mode. RI is a bill discount for a pay-as-you-go physical instance but not an actual physical instance, so it is also pay-as-you-go in essence. The pay-as-you-go instances must exactly match RI attributes to benefit from the billing discount during the RI term.
If the attributes of a pay-as-you-go physical instance in use match RI attributes, you can enjoy a bill discount. You can directly purchase and activate RI for existing instances or as new instances.
After prepaying a certain amount for RI, you can enjoy the corresponding discount within the purchase duration. Compared with the original monthly subscription and pay-as-you-go billing modes, the combination of RI and pay-as-you-go offers you the greatest discount possible to strike a balance between the flexibility and costs.
