To understand the related fees incurred by LVB recording more easily, you can use the following examples to estimate the resource usage and costs of the overall plan. The examples describe the [postpaid](#postpaid) billing mode for your reference.

## Background
User A runs an ecommerce platform. An ecommerce live streaming event was held for 10 days in November, and the live streams were recorded for playback on the purchase pages. The specific requirements are as follows:

<table>
<tr><th width="50%">Estimated LVB Resource Usage</th><th width="50%">Estimated VOD Resource Usage</th>
</tr><tr>
<td><ul style="margin:0">
<li>10 concurrent live streams per day
<li/>Live streaming bitrate: 1 Mbps
<li/>Watch duration per viewer: 2 hours
<li/>Average number of viewers: 1,000
<li/>All live streams were recorded in both HLS and MP4 formats
</ul></td>
<td><ul style="margin:0">
<li>Average daily number of viewers: 100
<li/>Video duration: 1 hour
<li/>Video bitrate: 500 Kbps
<li/>Video size: 10 GB 
<li/>Video storage duration: 3 months
</ul></td></tr></table>


## Postpaid Billing<span id="postpaid"></span>
This example mainly involves resource usages of LVB, LVB recording, and VOD as detailed below:

### LVB fees
- **Billing formula:** traffic = bitrate * average duration * average number of viewers.
- **Example analysis:**
	- Daily traffic usage ≈ 10 (streams) * 1 (Mbps) / 8 * 7200 (s) ** 1000 (viewers) = 9000000 (MB) = 9000 (GB).
	- 10-day LVB traffic fees ≈ 9000 (GB) * 0.0406 (USD/GB) * 10 (days) = 3654 (USD).

### LVB recording fees
- **Billing formula:**
	- Percentage of valid recording days = number of days when the recording feature is used in a calendar month / total number of days in the month.
	- Recording fees = peak number of concurrent recording channels in a calendar month * percentage of valid recording days * recording channel unit price.
- **Example analysis:**
	- Percentage of valid recording days = 10 (days) / 30 (days) = 1/3.
	- Recording fees for November = 10 (channels) * 2 (formats) * 1/3 * 5.2941 (USD/channel/month) = 35.294 (USD).

### VOD fees
- **Billing formula:**
	- Traffic = bitrate * duration * number of viewers.
	- Storage = storage volume * storage unit price.
> ? You can query the bitrate of the preset template in [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059). You can also define the bitrate of the template.	
- **Example analysis:**
	- Daily traffic usage ≈ 500/8 (Kbps) * 3600 (s) * 100 (viewers) = 22500000 (KB) = 22.5 (GB); approximate traffic fees for 30 days ≈ 22.5 GB * 0.038 USD/GB * 30 = 25.65 USD.
	- Storage fees ≈ 10 (GB) * 0.0009 (USD/GB/day) * 90 (days) = 0.81 USD.
Total VOD fees ≈ 25.65 + 0.81 = 26.46 USD.

>? Total fees = LVB resource fees + LVB recording fees + VOD resource fees = 3654 + 35.294 + 26.46 = 3715.754 USD.
