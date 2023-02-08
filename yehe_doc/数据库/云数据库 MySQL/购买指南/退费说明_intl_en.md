
- Monthly subscription (prepaid): You can return TencentDB for MySQL instances and request a refund (non-full).
- Pay-as-you-go (postpaid): TencentDB for MySQL will return resources directly, and no refund can be requested.
You can return monthly subscribed and pay-as-you-go instances in the instance list in the [TencentDB for MySQL console](https://console.tencentcloud.com/cdb/instance?language=en).

## Returning Instances
- When a monthly subscription instance is returned and its status has changed to **Isolating**, it will no longer generate fees.
- After an instance is terminated, its data will not be recoverable. You need to back up the data in advance.
- As database backups will be deleted when an instance is terminated, you need to download the backups in advance.
- As database audit will be deleted when an instance is terminated, you need to download the the database audit log in advance.
- After a monthly subscribed instance is terminated, its IP resources will be released simultaneously, and the instances cannot be accessed. If the instance has read-only or disaster recovery instances:
  - Read-only instances will be terminated at the same time.
  - Disaster recovery instances will disconnect their sync connections and be promoted to source instances automatically.
- When a monthly subscribed instance is returned, it is retained in the recycle bin for 7 days, where it cannot be accessed. To restore the instance, go to the recycle bin and renew it.
- Tencent Cloud has the right to reject any suspected abnormal or malicious application for return.
- Certain resources purchased during promotions may not be eligible for return. You can check the latest information on the official website.

## Standard Returns
Fees for consumed resources will be deducted from the refund. The remaining amount will be returned to your Tencent Cloud account by the proportion of the cash and voucher amount paid for the purchase.

#### Standard return policies
**Refund amount = Current Orders + Future Orders - Consumed Resources Fees**

- Current orders: The amount paid for current orders, excluding discounts and vouchers.
- Future orders: The amount paid for future orders, excluding vouchers.
- Fees for consumed resources are calculated based on the following policies:
 - For the used part, if the usage has lasted at least one month as of the date of downgrade, fees will be deducted by month; otherwise, fees will be deducted in a pay-as-you-go manner.
 - The usage is accurate down to the second
 - If the refunded amount ≤ 0, it is considered 0, and resources are deleted.

>!
>- Discounts and vouchers will not be returned.
>- The refund will be returned to your Tencent account by the proportion of the cash and free credit paid for the purchase.

## Related Operations
For more information on how to return instances in the console, see [Terminating Instance](https://www.tencentcloud.com/document/product/236/31895?lang=en&pg=).