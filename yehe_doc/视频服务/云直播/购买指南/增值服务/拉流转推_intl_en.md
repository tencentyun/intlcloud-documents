The relaying service allows you to quickly pull content from existing videos or live streams and push it to the destination address. The two billable items for the relaying service are [relay task duration](#time) and [third-party relaying bandwidth](#third_part).

## Supports and Limits
- The relaying service **has become a paid service since 00:00 (UTC+8) on July 1, 2021**. Relaying tasks executed after July 1, 2021 will incur relaying fees, regardless of when the tasks were created.
- Pulling data from an existing source will incur playback/download fees. If you pull from Tencent Cloud CSS, VOD, or COS, the billing rules of the corresponding product will apply.

[](id:time)
## Relay Task Duration
### Pricing
A relay task is billed by duration.

| Billable Item        | Price (USD/Min) |
| ---------------- | ----------------- |
| Relay task duration | 0.00032           |

### Billing details
- Billable item: Relay task duration
- Billing mode: Pay-as-you-go
- Billing cycle: Daily billing. The fees generated each day are deducted at 10:00 AM or whenever your daily bill is generated the following day.
- Billing rules: The fees are based on the duration in which relaying tasks are executed. Paused or expired tasks will not incur fees. If you resume a paused task, fees will be charged.

>! If pulling fails due to abnormal source contents, the relay task will not stop until the specified end time, and **the corresponding task duration will be billed**.


[](id:third_part)
## Third-Party Relaying Bandwidth
>! 
>- Relaying to a CSS URL of the current account (the account that created the relay task) will not incur relaying bandwidth fees.
>- Relaying to a non-CSS address will incur third-party relay fees.

### Pricing
Third-party relaying fees are based on the highest bandwidth (Mbps) used for relaying in each billing period. The price varies depending on the region to which your streams are relayed. If you relay to multiple regions in a billing period, fees will be charged separately based on the peak bandwidth usage in each region.

| Region             | Price (USD/Mbps/Month) |
| :--------------- | :------------------- |
| Chinese mainland | 12.67                |
| Hong Kong (China)        | 12.67                |
| Singapore           | 8.04                 |
| Frankfurt         | 7.1                  |
| Seoul             | 16.56                |
| India             | 23.66                |
| Thailand             | 13.01                |
| Silicon Valley         | 7.1                  |
| Virginia     | 7.1                  |
| Jakarta           | 17.4                 |
| Japan             | 13.01                |
| São Paulo           | 23.66                |
| Other regions             | 12.67                |




### Billing details
- Billing mode: Monthly pay-as-you-go
- Billing cycle: Monthly billing cycle. Your bill for each month is generated between the 1st and 3rd day of the following month.
- Billing rules: By default, third-party relay fees are charged in the pay-as-you-go mode based on your average daily peak bandwidth usage (for all third-party relay tasks) in each month. If a different billing mode is used for the LVB service under your account, that mode will apply to third-party relay.

