
## Billing Overview
TencentDB for MySQL offers the following two billing modes:  
- **Monthly subscription**: Fees are prepaid when an instance is created. This billing mode is suitable for business with stable needs in the long run as it is cheaper than pay-as-you-go billing. Moreover, the longer the service is purchased, the cheaper it is. For more information, see [Prepaid Billing Mode Description](https://intl.cloud.tencent.com/document/product/555/9618).
- **Pay-as-you-go**: In the pay-as-you-go (aka postpaid) billing mode, you can apply for resources for on-demand use and will be charged based on the actual usage at the billing time. It is suitable for instantaneously fluctuating businesses. In this mode, instances can be released immediately after the use so as to reduce the costs. For more information, see [Pay-as-you-go Billing Mode Description](https://intl.cloud.tencent.com/document/product/555/9617).


## Instance Price
To estimate the resource costs, you can directly calculate the package price of the required products with [TencentDB for MySQL Price Calculator](https://buy.cloud.tencent.com/price/cdb/).

>To help users further cut costs, TencentDB for MySQL has supported tiered pricing in the pay-as-you-go billing mode since July 15, 2016. The longer the service is used, the cheaper it is. Depending on the usage duration, the pay-as-you-go prices are divided into three tiers:
 - 0-4 days (within 4 * 24 hours): Tier 1 pay-as-you-go price applies.
 - 4-15 days (4 * 24 hours - 15 * 24 hours): Tier 2 pay-as-you-go price applies.
 - Over 15 days (over 15 * 24 hours): Tier 3 pay-as-you-go price applies.
 >
 >To obtain accurate price information, log in to your Tencent Cloud account.

## Calculation Method for Instance Upgrade Fees
If an instance will expire in T days, and the monthly fee difference between the target configuration and the current configuration is C, then the total upgrade fees will be T / 30 * C.


>- To ensure your business continuity, please upgrade your instance specification or purchase additional disk capacity in a timely manner before the disk capacity is used up. For more information, see [Upgrading TencentDB Instance Specification](https://intl.cloud.tencent.com/document/product/236/19707).
>- When the data size stored on an instance exceeds its capacity limit, the instance will be locked and become read-only (data writing is not allowed). You need to expand its capacity or drop some databases and tables in the console to unlock it.
>- To avoid the database from triggering the lock status repeatedly, a locked instance will be unlocked and allowed for reads and writes only when its remaining available capacity accounts for more than 20% of its total capacity or over 50 GB.


## Purchase Restrictions
In different billing modes, Tencent Cloud assigns each user different quotas of instances in each AZ.

Pay-as-you-go:
 - Before purchasing a TencentDB for MySQL instance, you need to verify your identity in your Tencent Cloud account; otherwise, you cannot purchase a pay-as-you-go instance. For more information, see [Identity Verification Guide](http://intl.cloud.tencent.com/document/product/378/3629).
 - You can purchase up to 10 pay-as-you-go instances in each AZ.


