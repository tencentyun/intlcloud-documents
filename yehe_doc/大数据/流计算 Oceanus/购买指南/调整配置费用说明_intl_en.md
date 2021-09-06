## Cluster Scale-out
Cluster scale-out means to increase the number of CUs. You can do so in the [Oceanus console](https://console.cloud.tencent.com/oceanus). During cluster scale-out, you need to pay for the configuration adjustment according to the remaining validity period of the cluster. The calculation rule for the scale-out fees of monthly subscribed clusters is as follows:
- Scale-out fees = number of new CUs * monthly unit price of CU * number of scale-out days / (365 / 12)
- Scale-out days = cluster expiration time - current time

>? Scale-out doesn't affect the expiration time of the cluster.

## Cluster Scale-in
When you scale in a cluster, the system will calculate the price difference according to the following formula:
**Refund = residual value of original configuration - purchase price of new configuration**

Involved amounts are as detailed below:
- Residual value of original configuration: refers to the effective order amount of the original configuration minus the used value of the original configuration.
- Effective order amount of original configuration: refers to the amount paid for the effective order, excluding discounts and vouchers.
- Used value of original configuration: for the used part, if the usage has lasted at least one month as of the date of downgrade, fees will be deducted by month; otherwise, fees will be deducted in a pay-as-you-go manner. **The usage is accurate down to the second.**
- Purchase value of new configuration: refers to the current official price of the new configuration multiplied by the remaining validity period.
  
>!
> - Deductions and vouchers are not refundable.
> - The refund will be credited to your account at the ratio of cash to trial credit paid upon purchase.
> - If the refund is ≤ 0, it will be calculated as 0.
