TencentCloud Managed Service for Prometheus (TMP) will change the free metric storage period of pay-as-you-go instances as described in [Free Metrics in Pay-as-You-Go Mode](https://www.tencentcloud.com/document/product/1116/43469) to **15 days** on **November 30, 2022**. **For TMP instances with storage period over 15 days, their metrics will be charged for the extra storage days**.

>? To check the free metrics you have used or streamline monitoring metrics to avoid unnecessary expenses, see [Streamlining Monitoring Metrics](https://www.tencentcloud.com/document/product/457/47004?lang=en&pg=).

## Storage Pricing

### Calculation formula
Storage fees = storage unit price * (data storage period - 15 days) * daily reported metric data volume in million entries

### Settlement cycle

Fees are settled on a daily basis.


### Storage unit price

| Region | Unit Price (USD/million entries) |
| :------------------------- | ---------- |
| Non-finance zones in the Chinese mainland, such as Guangzhou, Shanghai, and Beijing | 0.0015 |
| Regions outside the Chinese mainland + finance zones in the Chinese mainland, such as Hong Kong (China), Singapore, and Shenzhen Finance | 0.003 |

> ? Data entry count less than one million will be calculated as one million.

## Billing Example

Let’s suppose a user has purchased a TMP instance in a non-finance zone in the Chinese mainland, the data storage period is 45 days, and the number of reported metric data entries is 10 million a day, then:
The storage fees for that day = 0.0015 * (45-15) * 10 = 0.45 USD

