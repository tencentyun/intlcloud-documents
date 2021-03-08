The billable items of LVB recording include **LVB platform fees**, **VOD platform fees**, and **LVB recording fees**.
- For the billing mode of LVB, please see [LVB Pricing Overview](https://intl.cloud.tencent.com/zh/document/product/267/2819).
- For the billing mode of VOD, please see [VOD Pricing Overview](https://intl.cloud.tencent.com/document/product/266/2838).


## LVB Recording Fees

LVB recording is a paid feature, and **fees are calculated based on the peak number of concurrent LVB recording channels in the current month**. Detailed prices are as follows:

| Billable Item | Price | Settlement Cycle | Applicable Services |
| :----------- | :--------------- | :--------------- |  :--------------- |
| Recording channel peak | 5.2941 USD/channel/month | Monthly pay-as-you-go | LVB |

### Billing description

- Billable item: number of LVB recording channels.
- Billing mode: pay-as-you-go.
- Billing cycle: monthly billing cycle. The current month's bill will be generated between the 1st and 5th day of the next month. See the billing statement for details.
- Calculation formula:
  - Percentage of valid recording days = number of days when the recording feature is used in a calendar month / total number of days in the month.
  - Recording fees = peak number of concurrent recording channels in a calendar month * percentage of valid recording days * recording channel unit price.
>? Monthly peak number of concurrent recording channels: the greatest value among all 5-minute numbers of LVB recording channels in the month. One recording format is counted as one channel of recording stream. For example, if MP4 and HLS files are recorded for the same stream ID, they will be counted as two channels of recording streams.

  

### Billing example
Suppose you use the LVB recording service for 18 days between June 1 and July 1, 2021, and the recording channel peak for the month is 10, the LVB recording fees you need to pay on July 2, 2021 are as follows:

- Percentage of valid LVB recording days in June = 18 (days) / 30 (days) = 0.6.
- LVB recording fees for June = 5.2941 (USD/channel/month) * 0.6 * 10 (channels) = 31.7646 USD.

> !
>- The billing rule for the percentage of valid days will take effect on **November 1, 2020**, and bills will be generated on **December 1, 2020** according to this rule.
>- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. After enabling the recording feature, please make sure that your VOD service is in normal status. If it is not activated or is suspended due to overdue payment, LVB recording will not be available, no recording files will be generated, and no recording fees will be incurred.

