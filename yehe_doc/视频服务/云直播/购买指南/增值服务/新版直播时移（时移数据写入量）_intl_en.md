Time shifting is powered by the recording capability of CSS. It allows users to rewind and play earlier parts of a live stream. This is commonly used to play back highlights of live streamed sports events.


## Notes

- Time shifting is billed based on the traffic of live streams for which time shifting is enabled. Using this feature will also incur [playback traffic/bandwidth costs](https://intl.cloud.tencent.com/document/product/267/2819).
- Time shifting is disabled by default. You can enable it in the console or using a TencentCloud API.

[](id:price)
## Pricing

| Time-Shift Days | Price (USD/GB/Day) |
| ------------ | ---------------- |
| 1 day |  0.035  |
| 3 days | 0.052 |
| 7 days | 0.069 |
| 15 days | 0.12 |
| 30 days | 0.21 |

### Billing details

- Billable item: Live streaming traffic
- Billing mode: Pay-as-you-go
- Billing cycle: Daily. The time shifting fee generated each day will be deducted from your account the following day (the actual fee deduction and bill generation time may vary).


### Calculation formula

Time shifting fees = Live streaming traffic per day (GB) x Price (USD/GB/Day)


### Billing examples

Suppose a user created a time shifting template in the CSS console, bound it to a push domain, and started a live stream at 12:00, January 5. The live stream lasted for **five** hours. The video bitrate was 1 Mbps. The maximum number of time-shiftable days is seven days. 

Live streaming traffic = 1 Mbps x 18000 seconds ÷ 8 = 2.25 GB
Time shifting fee incurred on January 5 = 2.25 GB x 0.069 USD/GB = 0.15525 USD. The fee would be deducted on January 6.

Time shifting of the live stream is allowed from 12:00 on January 5 to 17:00 on January 12.