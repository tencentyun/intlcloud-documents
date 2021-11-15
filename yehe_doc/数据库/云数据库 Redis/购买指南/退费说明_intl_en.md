### Pay-as-you-go

Pay-as-you-go instances can be returned at any time by logging into to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and clicking **More** > **Terminate** next to the instance you wish to return on the instance list page.



## Monthly subscription

We offer two types of returns if you find yourself unsatisfied with your monthly subscription purchase.

 

## 5-day free returns
## Standard returns

 

The above methods can both be performed by logging into the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and clicking **Refund** on the instance list page.

### Return policy

1. When a monthly subscription instance is returned and its status has changed to **Terminating** or **Terminated**, it will no longer generate fees. 
2. When a monthly subscription instance is terminated, its IP address will be released, and the instance becomes inaccessible.
3. When a monthly subscription instance is returned, it is retained in the recycle bin for 7 days, where it cannot be accessed. To restore the instance, go to the recycle bin and renew it.
4. In the event that any return request is suspected to be abnormal/malicious, Tencent Cloud reserves the right to reject the request.

 

## 5-day free returns

If you are unsatisfied with your purchase, you can request for a free return within five days of purchase. 

 

- Each account can return **1** TencentDB for Redis instance within 5 (inclusive) days of purchase with no questions asked. Each account is given only one chance to use this type of return.

2. In the event that any return request is suspected to be abnormal/malicious, Tencent Cloud reserves the right to reject the request.

3. You will receive a full refund for the purchase, including the cash amount paid and gift cards used. 						

    > ***Note:** 
   >
   > - Rebates and vouchers will not be returned.
   >- The full refund will be returned to your Tencent Cloud account.

 

## Standard returns

If you have used up the one-time free return, you are still eligible for a standard return. 

 

1. Each account can return up to **199** instances as standard returns.
2. Fees for consumed resources will be deducted from the refund. The remaining amount, including cash credits and gift cards, will be returned to your Tencent Cloud account. 

 

### Use limits for standard returns
The following policies applies for standard returns:

 

1. Resources purchased during promotions might not be eligible for return.
2. Standard returns on the console are temporarily not supported for 256 MB instances using the standard Redis edition (with Redis 2.8 as the engine)

 

**Refund calculation for standard returns**
**Refund amount = Current Orders + Future Orders - Consumed Resources Fees**

 

Current orders: the amount paid for current orders, excluding discounts and vouchers.
Future orders: the amount paid for future orders, excluding vouchers.
Fees for consumed resources are calculated based on the following policies:

 

If the return request for the consumed resource is submitted a month after purchase, a monthly fee will be deducted. If the application is submitted within the month, fees will be deducted according to the pay-as-you-go billing mode.
- Billing is accurate to the second.
If the refunded amount ≤ 0, it is considered 0, and resources are deleted.

  ​						

> ***Note:**  							
>
> - Rebates and vouchers will not be returned.
>- The refund, including cash credits and gift cards, will be returned to your Tencent Cloud account.

 						

#### Sample refund calculation

 						

> Note: 							
>
> The prices used in the following examples are for demonstration purposes only. Please see the pricing page for actual prices.

 						

**5-day free return**
 Suppose a user purchases a standard edition instance with 2 GB memory in Guangzhou AZ 2 at 22 USD/month for 1 year at a 17% discount and used a $10 voucher.
Discounted price: 22 * 12 * (1 - 0.17) = $219.12
Amount paid: 219.12 - 10 = $209.12
The user is unsatisfied and requests a return within 5 days of purchase. This is the first time the account has requested a return.
Refund amount = Actual amount paid = $209.12

**Standard return**
Suppose a user purchases a standard edition instance with 2 GB memory in Guangzhou AZ 2 at 22 USD/month for 1 year at a 17% discount and used a $10 voucher.
Discounted price: 22 * 12 * (1 - 0.17) = $219.12
Amount paid: 219.12 - 10 = $209.12


**Case 1**: The user requests a return within 5 days of purchase, and this is not the first time the account has requested a return. Their resource consumption totaled 48 hours.
Refund amount: 209.12 - 48 * 0.06 ($0.06 is the pay-as-you-go unit price for this configuration) = $206.24


**Case 2**: The user requests a return within 5 days of purchase, and this is not the first time the account has requested a return. Their resource consumption totaled 48 hours. Services were renewed for another year with a 17% discount, and the amount paid for the renewal was 219.12 USD.
Refund amount: 209.12 - 48 * 0.06 ($0.06 is the pay-as-you-go unit price for this configuration) + 219.12 (the amount paid for future orders) = $425.36.

 

**Case 3**: The user requests a return within 5 days of purchase, and this is not the first time the account has requested a refund. The instance configuration was upgraded after 12 hours of use. The amount paid for the upgrade was $10, and their resource consumption totaled 72 hours. 
Refunded amount: 209.12 - 12 * 0.06 ($0.06 is the pay-as-you-go unit price for this configuration) + 10 / 365 (daily unit price for the configuration upgrade) * (365 - 3) (number of days for which the upgrade has yet to take effect) = $218.3178082