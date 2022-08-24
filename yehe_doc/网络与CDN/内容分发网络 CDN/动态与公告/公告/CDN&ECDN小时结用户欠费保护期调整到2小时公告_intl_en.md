## Grace Period Adjustment

Tencent Cloud plans to shorten the grace period for CDN and ECDN service from 24 hours to 2 hours for users adopting **postpaid hourly billing**. When the eligible user accounts become overdue, and there is no available extra traffic packs, the CDN and ECDN service remain available for two hours, and then they are suspended. This is to help prevent the high bills incurred when a domain name is compromised by attacks, in which case the billing does not stop even your account is out of balance. 



## Scope

The adjustment is applicable to users who adopt postpaid hourly billing.

<img src="https://qcloudimg.tencent-cloud.cn/raw/065f421898bd262eedc59fd1ee5f7b8b.png" alt="image-20220606132446295" style="width:50%;" />



> ? View your payment and billing mode in the [CDN console - Overview](https://console.cloud.tencent.com/cdn).

- If hourly-billed CDN/ECDN services are activated after 00:00:00, July 11, 2022, the 2-hour grace period applies by default.
- If CDN/ECDN services are activated before 00:00:00, July 11, 2022, refer to the SMS, email, or Message Center for the effective time of the adjustment.

## Impacts

This adjustment does not affect your service billing amount and cycle.

#### Policies after the grace period

- The ECDN acceleration services for your domain names will be suspended directly.
- If you have available CDN traffic packs, the CDN acceleration services will continue to be available until those packs run out.

#### What is a grace period?

When your account is overdue, the CDN and ECDN services are still available during the grace period. 

- During the **grace period**, the CDN/ECDN acceleration services remain available and incur charges.
- After the grace period, the CDN/ECDN acceleration services for your domain names will be suspended.

