Powered by the recording capability of CSS, the time shifting feature allows viewers to rewind and play back a video stream from earlier time points. When time shifting is enabled for a VOD playback domain, TS segment URLs and TS files for the video are saved in VOD, and the user can play back earlier video content by passing a time parameter in the request URL under the playback domain.

### Notes

- The time shifting feature is billed according to the **total time-shift period**. You will also be charged [playback fees](https://intl.cloud.tencent.com/document/product/267/2818) based on the traffic/bandwidth consumed, [live recording fees](https://intl.cloud.tencent.com/document/product/267/39605), and [VOD storage fees](https://intl.cloud.tencent.com/document/product/266/2838).
- **Total time-shift period** = **Total time-shift video length** (minutes) x **Time-shift days**
>?
>- Total time-shift video length: The total length (minutes) of the video files for which time shifting is enabled.
>- Time-shift days: The number of days during which time shifting is allowed. Value range: 1-30.

- Before using the time shifting feature, you need to enable **live recording** and **VOD storage** first. The videos recorded must be in HLS format, and the time-shift days cannot be more than the storage days.
- You need to submit a ticket to enable the time shifting feature. For details, see [Time Shifting](https://intl.cloud.tencent.com/document/product/267/31565). When you no longer need to use the feature, to avoid incurring unexpected charges, please submit a ticket to disable it.



[](id:price)

### Pricing

| Billable Item           | Price (USD/(Min x Day)/Day) |
| ------------ | ---------------- |
| Total time-shift period | 0.00003                |

### Billing details

- Billable item: Total time-shift period
- Billing mode: Pay-as-you-go
- Billing cycle: Daily. The time shifting fee generated each day will be deducted from your account the following day. For the actual fee deduction and bill generation time, see your billing statement.


### Calculation formula

- Total time-shift period = Total time-shift video length (minutes) x Time-shift days
- Time-shift fee = Total time-shift period x Unit price


### Pricing examples

A customer hosted a **five-hour** live streaming session starting from 12:00 on June 1 and allowed time shifting for the live stream for **10 days**.


Total time-shift period = 5 x 60 x 10 = 3,000 minutes
Time-shift fee incurred on June 1 = 0.00003 x 3,000 = 0.09 USD. The fee would be billed and deducted on June 2.
The live stream is playable from 12:00 on June 1 to 17:00 on June 11.