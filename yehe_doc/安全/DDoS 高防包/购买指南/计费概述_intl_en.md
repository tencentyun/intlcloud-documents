Tencent Cloud Anti-DDoS Pro has adopted new billing rules from **March 24, 2022**.
## Billing Mode

The new Anti-DDoS Pro service guarantees an all-out protection capability. Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack. In addition, the all-out protection will be enhanced along with the advance of Tencent Cloud network capabilities, and for which no extra upgrade costs are required.

>! Tencent Cloud reserves the right to restrict the traffic if the DDoS attacks on your business affect the infrastructure in the Tencent Cloud Anti-DDoS cleansing center. If the traffic of your Anti-DDoS Pro instance is restricted, your business may suffer the problems such as limited or blocked business access traffic.


| Billable Items      | Billing Mode  | Payment Method | Payment Description                                                       |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Number of protected IPs | Monthly subscription | Pay-as-you-go| Please select the number of business IPs to be protected by an Anti-DDoS Pro instance. Specification: 10 (default), 50, and 100.</br>If you need the protection for more IPs, extra fees will be charged. The number can only be increased but not decreased. |
| Protection bandwidth | Monthly subscription | Pay-as-you-go   | The protection bandwidth refers to the amount of your bandwidth used to protect and is billed by 95th percentile. The unit price is $14/Mbps/month. <br/>Anti-DDoS Pro allows you to exceed your plan’s limit, but the all-out protection capability will become not available and only the basic protection capability remains when the limit has been exceeded for 36 hours. |


>?
>- To use an Anti-DDoS Pro instance, please select the same instance region as your other Tencent Cloud resources such as CVM or CLB instances, and bind it to your business IP first.
>- 95th percentile bandwidth: In each calendar month, the inbound/outbound bandwidth is sampled every 5 minutes and the maximum is taken as the peak bandwidth on each day. At the end of the month, the sampled values are sorted from highest to lowest, and the top 5% are removed. The highest value in the remaining values is the billable bandwidth of the month.
## Pricing

A new Anti-DDoS Pro instance protects business IPs in the same region by default, and the number of protected IPs can be increased. If you need protection for multiple IPs in different regions, you need to purchase multiple instances. If you find the specifications are not ideal, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for customization.

### Protection bandwidth

| Protection Bandwidth | Unit Price for Monthly Subscription (in USD) |
| -------- | -------------------- |
| 50 Mbps   | 700                  |
| 100 Mbps  | 1,400                 |
| 200 Mbps  | 2,800                 |
| 300 Mbps  | 4,200                 |
| 500 Mbps  | 7,000                 |
| 600 Mbps  | 8,400                 |
| 800 Mbps  | 11,200                |
| 1,000 Mbps | 14,000                |
| 2,000 Mbps | 28,000                |
| 3,000 Mbps | 42,000                |

### Protected IP

| Number of Protected IPs   | Unit Price for Monthly Subscription (in USD) |
| ------------ | -------------------- |
| 10  | 8,890                 |
| 50  | 17,780                |
| 100 | 33,333.33             |


>?
>- For a 10-IP plan, 50 Mbps of protection bandwidth is offered for free by default.
>- For a 50-IP plan, 300 Mbps of protection bandwidth is offered for free by default.
>- For a 100-IP plan, 1,000 Mbps of protection bandwidth is offered for free by default.

### Anti-CC attack protection cap

|Region|Anti-CC Attack Protection Cap|
| ---- | ----------- |
|Guangzhou|300,000 QPS|
|Shanghai|700,000 QPS|
|Beijing|300,000 QPS|

The unit prices of the Anti-DDoS Pro instance are as follows:

### Anti-CC attack protection cap

|Region|Anti-CC Attack Protection Cap|
|----|---|
|Guangzhou|300,000 QPS|
|Shanghai|700,000 QPS|
|Beijing|300,000 QPS|

## Arrears Notification
For Anti-DDoS Pro instances:
- If the account balance is sufficient, the system will automatically settle the fees for the previous month and deduct them on the 1st of the following month.
- If the account balance is insufficient, the system will remind you to top up the account via the channel you configured (email, SMS, and Message Center).

>! 
>- Anti-DDoS Advanced (Global Enterprise Edition) is a pay-as-you-go service that is billed monthly. The minimum subscription term is 12 months. Upon expiry, your subscription will be auto-renewed unless canceled by [contacting us](https://intl.cloud.tencent.com/contact-us). Your instances cannot be terminated during a subscription term.
>- Make sure that you have three-month credit to be frozen when activating this service.
>- Payments for this service are not refundable.

## Service Termination
Anti-DDoS Pro adopts a pay-as-you-go model. If you want to end the service, you need to [submit a ticket](https://console.cloud.tencent.com/workorder/category) to terminate your instances. Otherwise, charges are still be incurred.
- After you apply for a termination in the current month, the monthly-subscribed items will be settled as usual, while the daily billable items are settled based on the actual usage. After you terminate your instances, the service will be stopped immediately and the instances will no longer be billed for the next month.
- The entire termination takes 1-3 working days to complete and is subject to the actual operation (protection fees may be incurred during the period).
