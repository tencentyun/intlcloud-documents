The relaying service allows you to quickly pull content from existing videos or live streams and push it to the destination address. The two billable items for the relaying service are [relay task duration](#time) and [third-party relaying bandwidth](#third_part).



## Notes
- The relaying service **has become a paid service since 00:00 (UTC+8) on July 1, 2021**. Relaying tasks executed after July 1, 2021 will incur relaying fees, regardless of when the tasks are created.
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
>- Relying to an address that is not a CSS URL of the current account will incur third-party relay fees.
>- We will adjust the pricing of relaying to third parties **starting from 00:00 (UTC+8) on August 1, 2022**. For details, see [CSS to Adjust Pricing of Third-Party Relay](https://intl.cloud.tencent.com/document/product/267/48434).

### Pricing

| Billable Item       | Price (USD/Mbps/Month) | Description              |
| :------------- | :------------------- | :------------------------- |
| Relay to third parties | 12.67        | Billed by bandwidth usage |


### Billing details
- Billing mode: Monthly pay-as-you-go
- Billing cycle: Monthly billing cycle. Your bill for each month is generated between the 1st and 3rd day of the following month.
- Billing rules: By default, third-party relay fees are charged in the pay-as-you-go mode based on your average daily peak bandwidth usage (for all third-party relay tasks) in each month. If a different billing mode is used for the LVB service under your account, that mode will apply to third-party relay.


