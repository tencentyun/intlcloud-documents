CSS can record live streams and store them in VOD. Using live recording will incur fees. Live recording is billed by **the peak number of concurrent recording channels of the month**.

### Notes

- The recording feature is disabled by default and can be enabled in the console or through TencentCloud APIs.
- The recorded video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default and will incur [VOD fees](https://intl.cloud.tencent.com/document/product/266/2838). After you enable the recording feature, please make sure that your VOD service is in a normal state. If it is not activated or is suspended due to overdue payments, live recording will not be available, no recording files will be generated, and no recording fees will be incurred.
- For more information on how to calculate the peak number of recording channels, please see [CSS Billing](https://intl.cloud.tencent.com/document/product/267/32479).



### Pricing

| Billing Item | Price (USD/Channel/Month) |
| ------------ | ------------------ |
| Peak number of recording channels | 5.2941             |

### Billing Overview

- Billable item: Number of live recording channels.
- Billing mode: Pay-as-you-go.
- Billing cycle: Monthly billing cycle. The current month's bill will be generated between the 1st and 5th day of the next month. Please refer to your actual billing statement for details.


### Calculation Formula

- Percentage of valid recording days = Number of days when the recording feature is used in a month / Total number of days in that month.
- Recording fees = Peak number of concurrent recording channels in a month × Percentage of valid recording days × Recording channel unit price.
>? Monthly peak number of concurrent recording channels: the greatest value among all 5-minute numbers of live recording channels in the month. One recording format is counted as one recording stream channel. For example, if MP4 and HLS files are recorded for the same stream ID, they will be counted as two recording stream channels.

### Billing Example

A recording template is configured by user A for domain names A and B in the CSS console with **1** recording file format for the former and **2** formats for the latter. Domain name A has 11 live pushes on April 2, 2020 and has 10 pushes on the other 5 days. Domain name B has 1 live push on April 29, 2020. The following table shows the number of days when domain names A and B use the recording feature: 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">Stream ID</th>
<th colspan=7 width="50%" style="text-align:center;">April 2020 (1st - 30th)</th>
<th rowspan=2 width="10%" style="text-align:center;">Number of valid days <br>when the recording feature is used</th>
</tr><tr>
<td style="text-align:center;">1st</td><td style="text-align:center;">2nd</td><td style="text-align:center;">3rd</td>
<td style="text-align:center;">…</td>
<td style="text-align:center;">28th</td><td style="text-align:center;">29th</td><td style="text-align:center;">30th</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">Recording is not used</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">User A uses <br>the recording feature</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- The number of peak recording channels on April 2, 2020 is **11**. Calculation formula: 11 Channels for domain name A × 1 Format + 0 Channels for domain name B × 2 Formats = 11 Channels.
- The number of peak recording channels on April 29, 2020 is **12**. Calculation formula: 10 Channels for domain name A × 1 Format + 1 Channel for domain name B × 2 Formats = 12 Channels.
- In April 2020, the number of recording days is 6 for domain name A and 1 for domain name B, so the total number of days when user A uses the recording feature in April is 6, and the percentage of valid recording days is 6 days / 30 days = 0.2.

Therefore, the maximum number of concurrent live push channels for April 2020 is 12, the percentage of valid recording days is 0.2, and the live recording fees you need to pay for this month are as follows:
Live recording fees for April = 5.2941 (USD/Channel/Month) × 0.2 × 12 Channels = 12.70584 USD.
