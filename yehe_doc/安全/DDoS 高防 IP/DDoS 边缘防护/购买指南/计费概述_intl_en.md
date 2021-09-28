## Billing Method
DDoS Edge Defender protects Tencent Cloud and non-Tencent Cloud business outside the Chinese mainland with unlimited times of protection. DDoS Edge Defender adopts a billing combination consisting of the basic protection plan plus user traffic usage.

| Billing Item       | Billing Mode     | Payment Mode | Payment Description                                                       |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Basic protection plan     | Monthly subscription     | Prepaid   | A total of ten instances with Anycast IP and CNAME record types can be created. Each instance is provided with 500 port forwarding rules and 500 domain name forwarding rules. |
| User traffic | Pay by traffic | Pay-as-you-go   | You will pay for the traffic you used. See below for details         |


## Billing Details
- Basic protection plan: 2770 USD/month for a root account
- Traffic pricing is based on a monthly cumulative tier as follows:

| Traffic Tier (USD/GB) | South America (SA) | Middle East (ME) | Asia Pacific Zone 3 (AP3) | Asia Pacific Zone 2 (AP2) | Asia Pacific Zone 1 (AP1) | Europe (EU) | North America (NA) | Africa (AA) |
| ----------------- | ------- | ------- | ----------- | ----------- | ----------- | ------- | ------- | ------- |
| 0–2 TB             | 0.128 | 0.162 | 0.12     | 0.108     | 0.094     | 0.071  | 0.071  | 0.128  |
| 2–10 TB            | 0.122  | 0.151  | 0.115      | 0.102      | 0.086      | 0.063  | 0.063  | 0.122  |
| 10–50 TB           | 0.115  | 0.1742 | 0.111      | 0.095      | 0.08       | 0.057  | 0.057  | 0.115   |
| 50–100 TB           | 0.109  | 0.132  | 0.105      | 0.086      | 0.074      | 0.051  | 0.051  | 0.109  |
| 100–500 TB         | 0.098  | 0.118  | 0.089    | 0.072      | 0.066      | 0.04   | 0.04   | 0.098  |
| 500–1000 TB        | 0.094  | 0.114  | 0.085      | 0.068      | 0.062       | 0.035  | 0.035  | 0.094  |
| > 1 PB             | 0.089  | 0.109  | 0.08       | 0.063      | 0.057      | 0.031   | 0.031   | 0.089  |

## Billing Sample
Assume that you have purchased DDoS Edge Defender service and consumed 4 TB of traffic (1 TB consumed in SA and 3 TB consumed in AP3) in the current month, the billing formula is as follows:
- Basic protection plan (prepaid): 2770 USD
- User traffic (pay-as-you-go):
 - Traffic consumed in SA falls into the 0–2 TB tier, resulting in a charge of 128 USD (0.128 USD/GB * 1 TB).
 - Traffic consumed in AP3 falls into the 0–2 TB and 2–10 TB tiers, resulting in a charge of 355 USD (0.12 USD/GB * 2 TB + 0.115 USD/GB * 1 TB).
- The total cost is summed by the fixed cost of basic protection plan plus the traffic usage cost, that is 3253 USD (2770 USD + 128 USD + 355 USD).

