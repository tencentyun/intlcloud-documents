>! The consumption bill feature is currently in beta test. To try it out, contact your Tencent Cloud rep.
>

## Directions
- The consumption bill displays your monthly consumption, including consumption of pay-as-you-go resources and the amortized cost of monthly subscription resources. Due to amortization, the data is only for cost estimation and cannot be used for reconciliation. For reconciliation purposes, use cost bills and transaction details instead.
- Costs of pay-as-you-go resources are calculated based on your actual spend and are not amortized. Costs of monthly subscription resources are amortized by day and then calculated by month.
- You can view summary and analysis data by resource ID, product, project, region, consumption type, etc.


Compared with Consumption Details 1.0, the new consumption bill provides more detailed information. The main updates are as follows:

- Supports all products
- Supports pay-as-you-go and monthly subscription products
- Displays spend by voucher, complimentary cash, and cash
- Supports amortization for special scenarios such as refund, upgrade, and downgrade


## Amortization Rules
Cost is amortized based on the cost bill. Deductions are positive, and refunds negative. The vouchers, complimentary cash, and cash amounts used for purchase or deduction are recorded separately. The amortization rules are as follows:


#### Pay-as-you-go
- "Month" is the month when the consumption actually occurs, i.e., the month when the resource is actually used.
- The costs of pay-as-you-go resources are not amortized.


#### One-time purchase
- "Month" is the purchase month of the resource, and "start time" and "end time" are 00:00:00 and 23:59:59 on the day of purchase, respectively.
- The costs of one-time purchases (such as packages) are not amortized.

#### Purchase of monthly subscription resource
- The cost is amortized daily from the day of purchase until the day before the expiration of the resource. "Month" is the month in which the consumption occurs, and the "start time" and "end time" are 00:00:00 and 23:59:59 on the day of amortization, respectively.
- Based on the purchased period and cost, vouchers, complimentary cash, and cash are amortized separately and rounded to two decimal places. If daily cost is less than 0.01 USD per day after amortization, the cost will be amortized from the next day at 0.01 USD per day until it is fully amortized.


#### Renewal of monthly subscription resource
- The cost is amortized daily from the first day of the renewal period until the day before the expiration of the resource. "Month" is the month in which the consumption occurs, and the "start time" and "end time" are recorded as 00:00:00 and 23:59:59 on the day of amortization, respectively.
- Based on the renewed period and cost, vouchers, complimentary cash, and cash are amortized separately and rounded to two decimal places. If the daily cost is less than 0.01 USD per day after amortization, the cost will be amortized from the next day at 0.01 USD per day until it is fully amortized.


#### Upgrade of monthly subscription resource
- The cost is amortized daily from the day of upgrade until the day before the expiration of the resource. "Month" is the month in which the upgrade occurs, and the "start time" and "end time" are recorded as 00:00:00 and 23:59:59 on the day of amortization, respectively.
- Based on the upgraded period and cost, vouchers, complimentary cash, and cash are amortized separately and rounded to two decimal places. If the daily cost is less than 0.01 USD per day after amortization, the cost will be amortized from the next day at 0.01 USD per day until it is fully amortized.


#### Downgrade of monthly subscription resource
- 降配折算时长：延长的时长不做分摊处理。
- Refund for downgrade:
  - Refund is amortized daily according to the refund amount and resource validity period until the day before the expiration of the resource. "Month" is the month in which the downgrade occurs, and the "start time" and "end time" are recorded as 00:00:00 and 23:59:59 on the day of amortization, respectively.
  - Cost amortization before the downgrade remains unchanged. According to the order end time and cost, vouchers, complimentary cash, and cash are amortized separately and rounded to two decimal places. If the daily cost is less than 0.01 USD per day after amortization, the cost will be amortized from the next day at 0.01 USD per day until it is fully amortized.

#### Refund of monthly subscription resource
Cost amortization before the refund remains unchanged. Compensatory amortization and termination are performed on the day of refund. The refund amount (a negative number) and the unamortized cost of the resource are both counted into the amortization of the day of refund. The latter is called compensatory amortization. **Compensatory amortization = Order cost - amortized cost; Termination cost = Refund amount; Actual monthly consumption = Normal amortization + Compensatory amortization + Termination cost**.


## Consumption Type
**Amortization for renewal**
It refers to the amortized cost of a monthly subscription resource in the month of renewal.
For example, if you renewed a monthly subscription resource on August 20, 2019 for 2 months (the renewal duration was 61 days), and the renewal cost was 122 USD, then the type of the amortized cost from August 20 to August 31 was amortization for renewal, which was 122 USD / 61 days × 12 days = 24 USD.

**Amortization for historical renewal**
It refers to the amortized cost of a previously renewed monthly subscription resource in a later month.
For example, if you renewed a monthly subscription resource on July 10, 2019 for 2 months (the renewal duration was 62 days), and the renewal cost was 124 USD, then the type of the amortized cost from August 1 to August 31 and from September 1 to September 9 was amortization for historical renewal. The amortized cost for historical renewal for August was 124 USD / 62 days × 31 days = 62 USD, and that for September was 124 USD / 62 days × 9 days = 18 USD.

**Amortization for purchase**
It refers to the amortized cost of the purchase of a monthly subscription resource in the month of purchase.
For example, if you purchased a monthly subscription resource on July 20, 2019 for 1 month, and the purchase cost was 31 USD, then the type of the amortized cost from July 20 to July 31 was amortization for purchase, which was 31 USD / 31 days × 12 days = 12 USD.

**Amortization for historical purchase**
It refers to the amortized cost of a previously purchased monthly subscription resource in a later month.
For example, if you purchased a monthly subscription resource on July 10, 2019 for 2 months (the purchase duration was 62 days), and the purchase cost was 124 USD, then the type of the amortized cost from August 1 to August 31 and from September 1 to September 10 was amortization for historical purchase. The amortized cost for historical purchase for August was 124 USD / 62 days × 31 days = 62 USD, and that for September was 124 USD / 62 days × 9 days = 18 USD.

**Pay-as-you-go**
It refers to the cost of a pay-as-you-go resource in the month of use.
Assume that: 1. You used a daily pay-as-you-go resource from August 21 to August 31, 2019, and the cost incurred was 50 USD, then the cost type was pay-as-you-go, and the pay-as-you-go cost for August was 50 USD.
2. You used a monthly pay-as-you-go resource from July 1 to July 31, 2019, and the incurred cost was 80 USD, then the cost type was pay-as-you-go, and the pay-as-you-go cost for July was 80 USD.

**Compensatory amortization**
If you initiate a refund, but the resource cost has not been fully amortized, then the unamortized cost will be counted into the amortization of the day of refund. This is called supplementary amortization.
Assume that you purchased a resource for 6 months at 181 USD on January 1, 2019 (the purchase duration was 181 days) and requested refund (-30 USD) on May 10, 2019. As the 181 USD was not fully amortized, the unamortized amount was counted into the day of refund (May 10). This amortized cost was compensatory amortization. Your compensatory amortization for May was 181 USD − Amortized cost (130 USD) = 51 USD, and the termination cost for May was -30 USD.

**Termination cost**
It is a negative value and refers to the amortized cost of a refunded resource in the month of refund.
Assume that you purchased a resource for 6 months at 181 USD on January 1, 2019 (the purchase duration was 181 days) and requested refund (-30 USD) on May 10, 2019. The refund amount would be counted into the day of refund (May 10), and the termination cost for May was -30 USD.

**Amortization for upgrade/downgrade**
It refers to the amortized cost of upgrade/downgrade in a month.
For example, if you purchased a resource for 1 month at 42 USD on May 10, 2019 and upgraded it on May 20 (the upgrade duration was 21 days), then the amortized cost of upgrade for May (from May 20 to May 31) would be 42 USD / 21 days × 12 days = 24 USD, and that for June (from June 1 to June 9) would be 42 USD / 21 days × 9 days = 18 USD.
