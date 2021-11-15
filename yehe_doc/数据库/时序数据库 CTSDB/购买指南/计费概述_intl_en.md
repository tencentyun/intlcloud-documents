CTSDB currently supports the pay-as-you-go billing mode (you need to complete the identity verification first before you can purchase pay-as-you-go instances. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/378/3629" target="_blank">Identity Verification Guide</a>).  



## Pay-as-You-Go Tiered Pricing
CTSDB supports pay-as-you-go tiered pricing. The longer it is used, the cheaper it is.
Depending on the usage duration, the prices in pay-as-you-go mode divide into three tiers:

- 0–4 days (within 4 * 24 hours): tier 1 pay-as-you-go price applies.
- 4–15 days (4 * 24 hours–15 * 24 hours): tier 2 pay-as-you-go price applies.
- Over 15 days (over 15 * 24 hours): tier 3 pay-as-you-go price applies.

For specific prices, please see [Pricing](https://intl.cloud.tencent.com/document/product/1100/40934).

## Instance Renewal Management
The **Renewal Management** page provides features such as **Batch Renewal**, **Set Auto-Renewal**, and **Collective Expiry Date** for instances.

>!To ensure business continuity, upgrade your instance specification or purchase additional disk space in time before the disk space is used up. For more information, please see [Adjusting Database Instance Specification](https://intl.cloud.tencent.com/document/product/1100/40921).
When the size of the data stored on an instance exceeds its purchased capacity, the instance will be locked and become read-only, and you will not be able to write data to it. You need to expand its capacity or drop some databases/tables to unlock it.
