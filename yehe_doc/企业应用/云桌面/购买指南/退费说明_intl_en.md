- Monthly subscription (prepaid): Each account is entitled to one unconditional full refund within five days of purchasing a CVD instance. Non-full refunds will be provided for other refund requests.
- Pay-as-you-go (postpaid): CVD resources will be directly returned without refund.
You can return instances in the desktop list in the [CVD console](https://console.cloud.tencent.com/cvd) in a self-service manner.

To help you use CVD more easily, if you are dissatisfied after purchasing a monthly subscribed CVD instance, you can return it unconditionally within five days. The five-day unconditional return is available **only once for one CVD instance**. The paid effective amount will be refunded to your Tencent Cloud account. In addition, you can also perform a standard return. In this case, fees for consumed resources will be deducted from the refund, and **the refund amount will be returned to your account by the proportion of the cash and free credit paid for the purchase.**
>!
>- Discounts and vouchers will not be returned.
>- The refund will be returned to your Tencent Cloud account.


## Notes
- After creating a CVD instance, you cannot **terminate/return its disks separately**.
- CVD currently doesn't have a repossession mechanism. After the instance is terminated/returned, all its cloud disk data will be cleared and cannot be recovered. Ask the user to back up their data first.


## Five-Day Unconditional Return
If you are dissatisfied after purchasing a monthly subscribed CVD instance, you may be able to return it unconditionally within five days after purchase. The specific rules are as detailed below:
- You can return one monthly subscribed CVD instance unconditionally within five (included) days after purchase.
- For an order that meets the five-day unconditional return policy, the refunded amount is the total amount paid at the time of purchase, including the cash amount, earnings amount, and free credit amount.
- Tencent Cloud has the right to reject any suspected abnormal or malicious application for return.
- For detailed refund rules, see [Five-Day Unconditional Refund](https://cloud.tencent.com/document/product/555/7440#.E4.BA.94.E5.A4.A9.E5.86.85.E6.97.A0.E7.90.86.E7.94.B1.E5.85.A8.E9.A2.9D.E9.80.80.E6.AC.BE).

## Standard Return
For CVD orders that are not eligible for the five-day unconditional return policy, the refund policy is as follows:
* After you return a CVD instance in a self-service manner, once its status becomes **Terminating** or **Terminated**, it will no longer incur any fees for compute and storage resources.
* As of the day when the monthly subscribed CVD instance is refunded, if the usage has lasted for one month or longer, fees will be calculated at the corresponding monthly subscription price and discount listed on the official website; otherwise, fees will be calculated at the pay-as-you-go price, i.e., refund amount = paid amount - usage duration * pay-as-you-go price * applicable discount.
* If the refund amount of the monthly subscribed CVD instance is ≤ 0, it will be calculated as 0, and resources will be returned.
* For a returned pay-as-you-go instance, fees will be charged based on the actual usage upon return (with the usage duration accurate down to the second).
* You can return up to 199 monthly subscribed CVD instances under each account in the console.

## Return Examples
>!The following prices are for demonstration purposes only and do not reflect the actual pricing shown on the official website. If you make a return, the actual unit prices at the time of purchase shall apply, which may vary by region, promotional campaign, or policy.

### Scenario
| Region | Compute Resources | Storage Resources | Billing Mode | Applicable Discount |
| ----------------- | --------------- | ----------------- | --------------- | ----------------- |
| Guangzhou | CVD - Graphic G1_4-core 16 GB | System disk: SSD cloud disk of 100 GB; data disk: premium cloud disk of 200 GB | Monthly subscription | 15% off |

Order amount = CVD - Graphic G1_4-core 16 GB + SSD cloud disk of 100 GB (system disk) + premium cloud disk of 200 GB (data disk) = 1380 USD + 100 USD + 70 USD = 1550 USD.
The actual payment amount is 1550 USD * 1 month * 0.85 = 1317.5 USD.

### Five-day unconditional return
Suppose you are not satisfied with a CVD instance and want to return it within five days after purchase, and this is your first time returning an instance.
The refund amount will be the actual payment amount, i.e., 1317.5 USD.

### Self-service return
Suppose you have used an instance for 48 hours and want to return it within five days after purchase due to business changes. This is not your first time returning an instance, and the regular self-service return quota of 199 instances has not been used up under your account.
The refund amount is 1317.5 USD - 48 hours * 4.26 USD/hour * 0.85 = 1143.692 USD.  

>?4.26 USD/hour is the unit price for a pay-as-you-go instance of the same specification, including compute and storage resources.
