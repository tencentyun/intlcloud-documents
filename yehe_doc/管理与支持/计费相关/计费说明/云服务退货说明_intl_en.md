>? 
>- <b>Monthly subscription (prepaid)</b>: Five-day unconditional refunds are not available for monthly subscriptions. When you apply for a refund, the payment amount will be refunded to your Tencent Cloud account according to the remaining value of the monthly subscription.
>- <b>Pay-as-you-go (postpaid)</b>: Pay-as-you-go resources are automatically reclaimed by the corresponding cloud product, and no refund can be requested. The frozen amount in your account balance will be unfrozen after the resource is released. For details, see [Prepay Account Freeze](https://www.tencentcloud.com/document/product/555/12039).
>- If you encounter any issues during the refund process, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Refunds

- For products purchased as part of a promotional campaign, the refund policy of the specific campaign will apply. If the campaign policy denies refunds, no refund can be made.
- 切换计费模式并且已退款的资源，发起退款则不重复计算。（本句删除）
- Unit prices and discounts are subject to the current system offers.
- Currently, self-service refunds are not available for orders placed through sales promotions. You can submit a ticket to apply for a refund.
- Tencent Cloud has the right to reject a refund application if any abnormal or malicious activity is suspected.

## Refund amount and calculation methods

**Refund amount = paid order amount - consumed amount**
There are three methods used to calculate the consumed amount (specific methods for different products are described in their corresponding documentation).
1. For monthly subscriptions, the consumed amount is calculated based on how long the resource was used. For the portion of usage duration that spanned an entire month, the refund is deducted based on the current monthly subscription price and discounts; for additional usage, the refund is deducted according to pay-as-you-go rates. 
Consumed amount = Monthly subscription price x Number of full months of usage x Current system discount + Pay-as-you-go usage duration x Current unit price x Current system discount
2. The consumed amount is calculated based on the usage duration. 
Consumed amount = (Usage duration / Total duration of the package) x Original order price x Current system discount 
A usage duration less than one day will be calculated as one day, and the current system discount that matches the usage duration will apply.
3. The consumed amount is calculated based on the plan or package usage. 
Consumed amount = Used package amount x Unit price x Current system discount
Promo vouchers and discounts that were used during purchase are nonrefundable. Non-voucher payments will be refunded to your Tencent Cloud account according to the payment methods (cash or free credit) and ratios used to make the original payment.

## Refunds for downgraded instances

To downgrade an instance, you can apply for a refund first and then purchase a new instance at a lower configuration. Refund amount = Refund amount of the original instance - Price of the new instance. Note that promo vouchers and discounts that were used during purchase are nonrefundable. Non-voucher payments will be refunded to your Tencent Cloud account according to the payment methods (cash or free credit) and ratios used to make the original payment.
- The refund amount for the original instance is calculated according to the amount of resources already used.
- The purchase price of the new instance is calculated based on the new purchase price and discount.

## Refunds for upgraded instances

If you upgrade a monthly subscribed CVM instance, you can still apply for a refund after the upgrade.
- The refund amount of the originally purchased portion is calculated according to the unified policy of the platform.
- For the upgraded portion, the price difference between the original and upgraded specifications will be refunded after deducting the number of days the upgraded instance has already been used.

## Return method

Self-service refunds are available for some cloud products. If the product does not support self-service refunds, please submit a ticket to request a refund. Before applying for a refund, ensure that the product meets the refund conditions and make sure your data has been migrated.
