TencentCloud Managed Service for Prometheus (TMP) is available for purchase in many major regions, and the service price may change across regions depending on different promotional activities or pricing strategies.


## Pricing

### Calculation formula
**Total fees = daily reported metric data volume (in million entries) x unit price + traffic fees (currently free of charge)**

### Billable items

| Billable Item | Description |
| :--------- | :----------------------------------------------------- |
| Average reported metric data volume | Tiered pricing based on the reported metric data volume |
| Traffic | Public network traffic, which is currently free of charge |


### Free metrics
Some metrics are free of charge in the pay-as-you-go mode. For details, see [Free Metrics in Pay-as-You-Go Mode](https://intl.cloud.tencent.com/document/product/1116/43469).

### Instance price

###  Unit price for 15-day data storage

| Range of Average Reported Metric Data Volume (in million entries) | Unit Price (USD) |
| :------------------------- | --------- |
| 0-200 | 0.19 |
| 200-800                    | 0.12      |
| 800-1,500                   | 0.06      |
| Above 1,500                   | 0.05    |

###  Unit price for 30-day data storage

| Range of Average Reported Metric Data Volume (in million entries) | Unit Price (USD) |
| :------------------------- | --------- |
| 0-200                      | 0.22    |
| 200-800                    | 0.16      |
| 800-1,500                   | 0.11     |
| Above 1,500                   | 0.08    |

###  Unit price for 45-day data storage

| Range of Average Reported Metric Data Volume (in million entries) | Unit Price (USD) |
| :------------------------- | --------- |
| 0-200                      | 0.25    |
| 200-800                    | 0.2     |
| 800-1,500                   | 0.12    |
| Above 1,500                   | 0.09    |



## Billing Examples

**Example 1 (less than 200 million reported metric data entries):**

Suppose 60 million entries of metric data are reported a day, and the data retention period is specified as 15 days, then the daily fees = 60 × 0.19 = 11.4 USD.

Note: “60” in the above formula indicates 60 million metric data entries.

**Example 2 (more than 200 million reported metric data entries):**

Suppose 900 million entries of metric data are reported a day, and the data retention period is specified as 30 days, then the daily fees are calculated in a tiered manner as follows:
For the first 200 million metric data entries, the fees = 200 x 0.25 = 50 USD
For the 200-800 million metric data entries, the fees = (800 - 200) x 0.2 =120 USD
For the 800-900 million metric data entries, the fees = (900 -800) x 0.12 = 12 USD
Therefore, the total fees = 50 + 120 + 12 = 182 USD

Note: “900” in the above formula indicates 900 million metric data entries. 

## Relevant Documentation
- You can purchase TMP instances through the console. For more information, please see [Purchase Methods](https://intl.cloud.tencent.com/document/product/1116/43157).
- TMP sends alert messages to you before it expires and its resources are repossessed. For more information, please see [Payment Overdue](https://intl.cloud.tencent.com/document/product/1116/43158).
