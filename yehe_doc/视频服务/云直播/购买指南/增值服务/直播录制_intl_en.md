CSS can record live streams and store them in VOD. Using live recording will incur fees. Live recording is billed by **the peak number of concurrent recording channels during the month**.

### Must-Knows

- The recording feature is disabled by default and can be enabled in the console or through TencentCloud APIs.
- Recording files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default, which will incur [VOD fees](https://intl.cloud.tencent.com/document/product/266/2838). After you enable the recording feature, make sure that your VOD service is in a normal status. If it is not activated or is suspended due to overdue payments, live recording will not be available. No recording files will be generated. Nor will fees be incurred.
- For information on how to calculate the peak number of recording channels, see [CSS Billing](https://intl.cloud.tencent.com/document/product/267/32479).



### Pricing

| Billable Item | Price (USD/Channel/Month) |
| ------------ | ------------------ |
| Peak number of recording channels | 5.2941             |

### Billing details

- Billable item: The number of live recording channels.
- Billing mode: Pay-as-you-go.
- Billing cycle: Monthly. The recording fees incurred each month are deducted within the first five days of the following month. For details, see your billing statement.


### Calculation formula

- Percentage of recording days = Number of days the recording feature is used during a month / Total number of days in that month.
- Recording fees = Peak number of concurrent recording channels in a month x Percentage of recording days x Unit price.
>? The peak number of concurrent recording channels during a month is the highest number of recording channels occurring at the same time during the month (the data is collected every five minutes). Each recording format is counted as one recording channel. For example, if the same stream is recorded into MP4 and HLS, they will count as two recording channels.

### Billing examples

Suppose a user bound recording templates to domain A and domain B in the CSS console. According to the templates, the streams of domain A are recorded into **one** format and those of domain B are recorded into **two** formats. Domain A had 11 live streams on April 2, 2020 and 10 live streams on another five days of that month. Domain B had one live stream on April 29, 2020. The recording days of domain A and domain B in April would be as follows: 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">Stream ID</th>
<th colspan=7 width="50%" style="text-align:center;">April 2020 (1st - 30th)</th>
<th rowspan=2 width="10%" style="text-align:center;">Number of days <br>the recording feature is used</th>
</tr><tr>
<td style="text-align:center;">Day 1</td><td style="text-align:center;">Day 2</td><td style="text-align:center;">Day 3</td>
<td style="text-align:center;">…</td>
<td style="text-align:center;">Day 28</td><td style="text-align:center;">Day 29</td><td style="text-align:center;">Day 30</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">No recording tasks</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">Account-level usage</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- The number of peak recording channels on April 2, 2020 is **11** (11 channels for domain A x 1 format + 0 channels for domain B x 2 formats = 11 channels).
- The number of peak recording channels on April 29, 2020 is **12** (10 channels for domain A x 1 format + 1 channel for domain B x 2 formats = 12 channels).
- In April 2020, the number of recording days for domain A and domain B is 6 and 1 respectively. At the account level, the number of recording days is 6, and the percentage of recording days in April is 6 days / 30 days = 20%.

Therefore, the highest number of concurrent recording channels for April 2020 is 12, the percentage of recording days is 20%, and the live recording fees incurred is as follows:
Live recording fees for April = 5.2941 (USD/Channel/Month) x 0.2 x 12 channels = 12.70584 USD.


## Recording to COS

### Pricing

If you record CSS streams to COS, an additional fee will be charged based on the recording duration of each recording channel.

| Billable Item | Price (USD/Min/Month) |
| ----------------- | -------------------- |
| Recording to COS | 0.000096             |

### Billing details

- Billable item: Recording to COS
- Billing mode: Pay-as-you-go
- Billing cycle: Monthly. The recording-to-COS fees incurred each month are deducted within the first five days of the following month. For details, see your billing statement.

### Billing examples

Suppose a user bound recording templates to domain A and domain B in the CSS console. According to the templates, the streams of domain A are recorded into one format and those of domain B are recorded into two formats. Domain A had 10 live streams on January 13, 2023, which lasted for 30 minutes. Domain B had one live stream on January 20, 2023, which lasted for 20 minutes. The recording-to-COS fee incurred for January 2023 would be as follows:
`0.000096 (USD/min/month) x (10 channels x 1 format x 30 minutes + 1 channel x 2 formats x 20 minutes) = 0.03264 USD`

