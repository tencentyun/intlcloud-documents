The relaying service allows you to quickly pull content from existing videos or live streams and push it to the destination address. This service incurs three costs – the [relay task duration cost](#time), the [third-party relaying cost](#third_part), and an [extended feature cost](#value).

## Must-Knows
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

### Billing examples
Suppose you used the relay feature for 100 minutes on October 1, 2022. On October 2, 2022, you would need to pay the following relay task duration fee:
`0.00032 (USD/minute) x 100 (minutes) = 0.032 (USD)`


>! Even if pulling fails due to a source error, a relay task will not stop until the end time you specify, and **costs will be incurred during this period**.


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
- Billing cycle: Monthly billing. Your bill for each month is generated between the 1st and 3rd day of the following month.
- Billing rules: By default, third-party relay fees are charged in the pay-as-you-go mode based on your average daily peak bandwidth usage (for all third-party relay tasks) in each month. If a different billing mode is used for the LVB service under your account, that mode will apply to third-party relay.

### Billing examples
Suppose you used the relay feature to relay streams to third parties on five days in October 2022. The region you relayed to was the Chinese mainland, and the peak bandwidth used for relay on the five days were 10 Mbps, 80 Mbps, 70 Mbps, 75 Mbps, and 60 Mbps respectively.
Your LVB billing mode for the Chinese mainland is daily bill-by-bandwidth. There are 31 days in October.
Your third-party relay fee for October would be as follows:
`(10 Mbps + 80 Mbps + 70 Mbps + 75 Mbps + 60 Mbps）/31 days x 12.67 (USD/Mbps/month）= 120.569 USD`

[](id:value)
## Extended Feature Cost
Local mode for relay is an extended feature of CSS. If you enable local mode, the MP4 files of a relay task will be cached to the local node before they are relayed. This ensures smoother and more reliable playback.

### Notes
In addition to the extended feature cost for using local mode, there will also be [relay service fees](https://intl.cloud.tencent.com/document/product/267/41059).

### Pricing

| Type     | Price (USD/Unit) |
| ------------ | --------------------- |
| Unit price | 0.01515               |

**Ratio of billing duration to actual duration:**

| Extended Feature                   | Ratio<br>Billing Duration (Billing Unit) : Actual Duration (Minutes) |
| -------------------------- | ---------------------------------------------------------- |
| Local relay mode           | 0.02 : 1                                                   |

### Billing details
- Item: Extended feature
- Billing mode: Pay-as-you-go
- Billing cycle: Daily. The fee generated each day will be deducted from your account the following day. For the actual fee deduction and bill generation time, see your billing statement.


### Calculation formulas
- Billing duration = Actual duration x Ratio
- Fee = Unit price x Billing duration

### Billing examples
Suppose you enabled local mode for a relay task on November 23, 2022. The duration of the task was 100 minutes, including 60 minutes of local files. On November 24, you would need to pay the following fees:
- The relay fee: `0.00032 (USD/minute) x 100 (minutes) = 0.032 (USD)`
- The extended feature fee: `0.01515 (USD) x 0.02 (billing unit/minute) × 60 (minutes) =0.01818 (USD)`
