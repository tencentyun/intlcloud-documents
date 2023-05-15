TDSQL-C for MySQL supports **termination/refund** operations on clusters or instances under clusters in the console. This document describe the refund instructions.

- Monthly subscription (prepaid): For TDSQL-C for MySQL, each account is entitled to unconditional full refund only once within five days after purchase by default. Non-full refunds will be provided for other refund requests.
- Pay-as-you-go (postpaid): All TDSQL-C for MySQL resources can be returned directly, but there will be no refunds.
  The above operations can be performed in the [console](https://console.cloud.tencent.com/cynosdb): either on the **Cluster Management** page > Terminate/Refund** (tab view)** or **Cluster List** > **Operation** column > **More** > **Terminate/Refund** (list view)**.
  For the pay-as-you-go (postpaid) option, you will be charged based on your actual resource usage, and no refunds are involved. The following instructions are mainly for monthly subscribed clusters.

### Self-Service Returns
- After a monthly subscribed cluster is returned, it won’t be charged any more once its status changes to "Isolating" or "Isolated".
- When a monthly subscribed cluster is returned, it is retained in the recycle bin for 7 days, where it cannot be accessed. To restore the cluster, go to the recycle bin and renew it.
- When a monthly subscrbed cluster is terminated, its IP address will be released, and it becomes inaccessible.
- Tencent Cloud has the right to reject the application for any suspected exceptional or malicious returns.
- Certain resources purchased during promotions may not be eligible for return. You can check the latest information on the official website.

## Five-Day Free Returns
Tencent Cloud refund policy is applicable to the TDSQL-C for MySQL product. You can return your purchased TDSQL-C for MySQL clusters within 5 (inclusive) days with no questions asked.
- Each account can return **one** monthly subscribed TDSQL-C for MySQL instance unconditionally **within five (inclusive) days after purchase** by default.
- For clusters with billing mode switched from **Pay-as-You-Go** to **Monthly Subscription**, the five-day free returns are not supported.
- Tencent Cloud has the right to reject the application for any suspected exceptional or malicious returns.

#### Rules for five-day free returns
For an order eligible for 5-day free returns, the refund is **the total amount paid upon purchase**, including the amount of cash account, revenue account, and complimentary account.
>!
>- **Discounts and vouchers are not refundable.**
>- **All the **refund amount** will be credited into your **Tencent Cloud account**.

## Standard Returns
- If you have already returned an instance unconditionally within five days after purchase, you can also return **199 monthly subscribed instances** in a self-service manner at any time in the console.
Fees for consumed resources will be deducted from the refund. The remaining amount will be returned to your Tencent Cloud account by the proportion of the cash and voucher amount paid for the purchase.

#### Rules for standard returns
**Refund = currently effective order amount + ineffective order amount - used resource value**

- Current orders: The amount paid for current orders, excluding discounts and vouchers.
- Future orders: The amount paid for future orders, excluding vouchers.
- Fees for consumed resources are calculated based on the following policies:
 - For the used part, if the usage has lasted at least one month as of the date of downgrade, fees will be deducted by month; otherwise, fees will be deducted in a pay-as-you-go manner.
 - The usage is accurate down to the second.
 - If the refunded amount ≤ 0, it is considered 0, and resources are deleted.

>!
>- Discounts and vouchers will not be returned.
>- The refund will be returned to your Tencent account by the proportion of the cash and free credit paid for the purchase.

## Relevant Documents
- [Deleting Instance](https://intl.cloud.tencent.com/document/product/1098/44628)
- [Deleting Cluster](https://intl.cloud.tencent.com/document/product/1098/44619)
