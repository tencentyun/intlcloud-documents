This document describes the bandwidth-based pay-as-you-go billing mode of BWP.
>?
>- For detailed BWP pricing, see [Billing ‍Overview](https://www.tencentcloud.com/document/product/684/15254).
>- Bandwidth-based pay-as-you-go billing is only available for general BGP bandwidth packages.
>- ‍When a bandwidth package is activated, the bandwidth fee of one billing cycle is frozen from your account based on your selected bandwidth cap and the unit price. For details, see [Frozen Funds](https://www.tencentcloud.com/document/product/555/12039)‍.
>

## Billing description
- **Billing date**
The bill is issued on Day 1-2 of every month. You can check the details in Cost Center.
- **Settlement date**
Fees are calculated on a daily basis and automatically deducted from the account balance of the user.
- **Scope**
A bandwidth package is region-specific, which means it can only be used in one region.
- **Bandwidth cap**
 - Instance-based bandwidth cap: The bandwidth cap selected upon creation of the bandwidth package
 - Regional total bandwidth: For bandwidth limits of different line types, see [Use Limits](https://www.tencentcloud.com/document/product/684/15247).

## Fee calculation
**Bandwidth package fee** = The maximum bandwidth cap selected on the current day (Mbps) × billable period (days) × product unit price (USD/Mbps/day).
**Maximum bandwidth cap selected on the current day**: The highest bandwidth cap set for the bandwidth package in the settlement period.

**Billing duration**: The bandwidth-based fee is settled on a daily basis, and the minimum billable unit is one hour. See the billing example below.

## Billing example
Assume that on June 1st, you have a bandwidth-based pay-as-you-go general bandwidth package in Nanjing at a unit price of 0.55 USD/Mbps/day. The max bandwidth cap of the day is 80 Mbps. The package is created at 10:45:00 and deleted at 13:30:00, therefore the billable period is 3 hours. 
**Bandwidth package fee** = 80 × (3/24) x 0.55 = 5.5 USD

## See also
[Billing Overview](https://www.tencentcloud.com/document/product/684/15254)