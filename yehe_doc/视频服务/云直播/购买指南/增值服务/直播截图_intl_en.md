CSS can take screenshots of live streams and store them in COS. Using screencapture will incur fees, which will be billed **by the total number of screenshots taken for the month**.

### Notes

- Screencapture is disabled by default and can be enabled in the console or through cloud APIs.
- The generated screenshots are stored in COS and will incur COS storage fees. For details, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).
- Screencapture is a paid feature. **The first 1,000 screenshots of each month are free. Any additional screenshots taken will incur fees**.



### Pricing

| Screenshots | Price (USD/Thousand screenshots) | Notes |
| -------- | ----------------- | ------------------------ |
| ≤ 1000 |0 | The first 1,000 screenshots of each month are free |
|＞ 1000|0.0176| The total number of screenshots will be rounded up to the nearest 1,000 |

### Billing Overview

- Billable item: the number of screenshots.
- Billing mode: pay-as-you-go.
- Billing cycle: monthly billing cycle. The current month's bill will be generated between the 1st and 5th day of the next month. Please refer to your actual billing statement for details.
- Billing rules: fees are calculated by multiplying the total number of screenshots taken in a month and the unit price.



### Billing Example

Suppose you used the live screencapture service from January 1 to February 1, 2021, and a total of 168,000 screenshots were generated during the month. Then, the live screencapture fees you would need to pay on February 2, 2021 would be as follows:
Live screencapture fees for January = 0.0176 (USD/Thousand screenshots) × (168 - 1) Thousand screenshots = 2.9392 USD.