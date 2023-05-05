COS supports self-service refunds for resource packs. Before you request a refund, read [Refund rules](#rule) first.

## Refund Policy

<span id="rule"></span>

### Refund rules

1. Vouchers used for purchasing a resource pack are not refundable. Non-voucher fees will be refunded to the payer's Tencent Cloud account in accordance with the payment mode (cash or gift card) and payment ratio. For more information, see [Order Management](https://console.cloud.tencent.com/expense/deal).
2. A self-service refund is supported if the COS resource pack meets the following three conditions:
 - Order type: **Purchase** or **Renew**.
 - Usage: The resource pack has not been used.
 - Validity period: The resource pack is within the validity period if purchased or has not taken effect if renewed.

>!
>- If the policy of the campaign where the resource pack was purchased conflicts with the refund policy, the former shall prevail.
>- We may reject a refund request if we suspect refund abuse.
>- Whether a resource pack configured to take effect at the specified time is eligible for a refund is subject to the availability of the operation in the console.

### FAQ

#### 1. How do I view the order type of a resource pack?
Go to [**Billing** > **Billing Center** > **Order Management** > **Prepaid Order**](https://console.cloud.tencent.com/expense/deal) and set **Product Category** to **COS** to view the order type of the target resource pack.


#### 2. How do I view the usage and validity period of a resource pack?
In the COS console, go to [Resource Packs > Purchased](https://console.cloud.tencent.com/cos/package/buy) to view the usage and validity period of the target resource pack.



### Refund entry

- For purchased resource packs
You can request a refund on a resource pack eligible for a self-service refund on the **Resource Packs** page in the **COS console**. For detailed directions, see [Requesting a refund on a purchased resource pack](#new).
- For renewed resource packs
You can request a refund on a resource pack eligible for a self-service refund on the **Renewal Management** page in the **Billing Center**. For detailed directions, see [Requesting a refund on a renewed resource pack](#renewal).


### Method for calculation of the refunded amount

Refunded amount = paid amount - (used duration/total duration) * original order price * applicable discount

>?
> - The used duration is the period of time from purchase to refunding. A used duration less than one day will be calculated as one day.
> - The original order price is calculated based on the specification, purchase duration, and pay-as-you-go unit price.
> - The applicable discount is subject to factors such as the duration the resource has been used and the discount offered to you.
> 

### Calculation example for a self-service refund

Assume that you purchased a STANDARD storage pack of 50 GB for regions in the Chinese mainland with a validity period of six months on the COS resource pack purchase page for 3.46 USD in cash, with no vouchers available. On the day of purchase, the resource pack was not used and was eligible for a self-service refund, and you requested a self-service refund. Then, the method for calculation of the refunded amount is analyzed as follows:

- The original order price is 50 GB * 6 months * 0.024 USD/GB/month = 7.2 USD.
- A used duration less than one day will be calculated as one day.

Refunded amount = 3.46 - (1/180) × 7.2 = 3.42 USD.


## Directions

### Requesting a refund on a purchased resource pack[](id:new)

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Resource Packs** > **Purchased** to enter the purchased resource pack management page.
3. Find the target resource pack and click **Refund** on the right.
>!Usage statistics are not real-time data (delayed for 24 hours). The usage of a resource pack on the day of purchase is not displayed until the next day.
>
4. On the refund information page, carefully check the refund information, including the resource pack information, form of refund, and refunded amount.
5. After confirming that everything is correct, click **Confirm** to submit your request.
 - After you submit a self-service refund request, the system will refund your money and terminate the cloud resource in three to five minutes.
 - You can view the refund order at [Order Management](https://console.cloud.tencent.com/expense/deal). When the order status changes to **Refunded**, you can check the amount in the Billing Center.

### Requesting a refund on a renewed resource pack[](id:renewal)

1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com).
2. In the top-right corner of the console, click **Billing** > **Billing Center** > **Renewal Management**. Set **Product Category** to **COS**. Select **Manual Renewal** or **Auto-Renewal** as the renewal type filter and find the target resource pack. In the **Operation** column of the renewal list, click **More** > **Opt out of Renewal** .

  - A self-service refund is available for an eligible resource pack.
  - A refund is unavailable for a resource pack that is not eligible.
>!Usage statistics are not real-time data (delayed for 24 hours). The usage of a resource pack on the day of purchase is not displayed until the next day.
>
3. On the refund information page, carefully check the refund information, including the resource pack information, form of refund, and refunded amount.
4. After confirming that everything is correct, click **Confirm** to submit your request.
 - After you submit a self-service refund request, the system will refund your money and terminate the cloud resource in three to five minutes.
 - You can view the refund order at [Order Management](https://console.cloud.tencent.com/expense/deal). When the order status changes to **Refunded**, you can check the amount in the Billing Center.
