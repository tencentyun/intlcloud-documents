CSS provides porn detection. Because CSS needs to take screenshots in live streams to detect pornographic content, using porn detection will incur [porn detection fees](#check_price) and [screencapture fees](https://intl.cloud.tencent.com/document/product/267/39606). Porn detection is a paid feature and is **billed by the total number of porn detection screenshots taken for the month**.

### Notes

- Porn detection is disabled by default and can be enabled in the console.
- The generated screenshots are stored in COS and will incur COS storage fees. For details, please see [COS Pricing](https://intl.cloud.tencent.com/pricing/cos).
- Porn detection is a paid feature. **The first 1,000 porn detection screenshots of each month are free. Any additional screenshots taken will incur fees**.



[](id:check_price)

### Pricing


| Porn Detection Screenshots | Price (USD/Thousand screenshots) | Notes |
| -------- | --------------- | ------------------------ |
| ≤ 1000 |0 | The first 1,000 screenshots of each month are free |
|＞ 1000|0.2294| The total number of screenshots will be rounded up to the nearest 1,000 |

>? 
>- For screenshots stored in [COS](https://intl.cloud.tencent.com/document/product/436/6222) outside the Chinese mainland, additional public network downstream traffic fees will be incurred. For the detailed prices of specific billable COS items, please see [COS Pricing](https://buy.cloud.tencent.com/price/cos/overview).
>- For regions that support live screenshot storage, please see [Service Region](https://intl.cloud.tencent.com/document/product/267/38285).

[](id:description)

### Billing Overview

- Billable item: number of screenshots for porn detection.
- Billing mode: pay-as-you-go.
- Billing cycle: monthly billing cycle. The current month's bill will be generated between the 1st and 5th day of the next month. Please refer to your actual billing statement for details.
- Billing rules: fees are calculated by multiplying the total number of screenshots (with the first 1,000 free screenshots deducted) taken in a calendar month for porn detection and the unit price.

[](id:example)

### Billing Sample

Suppose you used the porn detection service from January 1 to February 1, 2021, and a total of 168,000 screenshots for porn detection were generated during that month. Then, the porn detection fees you would need to pay on February 2, 2021 would be as follows:
Porn detection fees for January = 0.2294 (USD/Thousand screenshots) × (168 - 1) Thousand screenshots = 38.3098 USD.
