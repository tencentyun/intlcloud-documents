## Billing Mode for Upgraded Instances
- If you upgrade a monthly subscribed database instance, the price difference between original and upgraded specifications is deducted from your account. If the account balance is insufficient, you need to top it up. The upgraded instance will be billed by the new specification.
- When a pay-as-you-go instance is upgraded, it will be billed based on the new specifications in the next billing cycle.

## [Billing Method for Downgraded Instances](id:degrade_billing)
### Billing Description for Downgrade
#### Monthly subscription
If you degrade a monthly subscribed database instance, the price difference is calculated according to the following formula:
**Refund amount = Remaining amount for the original configuration - Purchase price of the new configuration**

Description:
- Remaining amount for the original configuration: The amount obtained by **the effective order amount of the original configuration minus the consumed amount for the original configuration.
- The effective order amount of the original configuration: The amount paid for the order in effect, excluding discounts and vouchers.
- The consumed amount for the original configuration is calculated based on the following rules:
 - For the used part, as of the day when downgrade is initiated, if the usage has lasted for one month or longer, fees will be deducted by month; otherwise, fees will be deducted in a pay-as-you-go manner.
 - The usage is accurate down to the second.
- Purchase price of the new configuration: The current official price of the new configuration x the remaining usage duration.
>!
>- Discounts and vouchers will not be returned.
>- The refund will be returned to your Tencent Cloud account by the proportion of the cash and free credits paid for the purchase.
>- If the refund amount is ≤ 0, it will be calculated as 0, that is, the refund amount will be 0.

#### Pay-as-you-go
If you choose to degrade a pay-as-you-go database instance, it will be billed at the tier 1 pay-as-you-go price for the new configuration.

## Relevant Documentation
TencentDB for MySQL supports flexible scaling that allows you to quickly adjust instance specifications. For related operations, see [Adjusting Database Instance Specification](https://www.tencentcloud.com/document/product/236/19707?lang=en&pg=)
