The LVB fees consist of basic, value-added, and extended service fees, as shown below:

![img](https://main.qcloudimg.com/raw/67a295effc191c4f710d9e2622fa1b01.png)

- [Basic service fees](#base): incurred by live streaming resource consumption when LVB is used. You can switch between the traffic and peak bandwidth billing modes.
- [Value-added service fees](#appreciation): incurred when value-added features such as LVB transcoding, recording, screenshotting, and porn detection are used. Such features are disabled by default and only incur fees when used.
- [Extended service fees](#extensions): incurred by use of value-added features provided jointly by LVB and other Tencent Cloud services. Each Tencent Cloud service will be charged by its respective billing rule.


## Basic Service Fees
<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td>LVB traffic (default)</td>
<td>If the billing mode is <b>daily bill-by-traffic</b>, the LVB fees will be <strong>billed by the consumed traffic</strong>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">Daily postpaid</a></td>
</tr><tr>
<td>LVB bandwidth peak</td>
<td>If the billing mode is <b>daily bill-by-bandwidth</b>, the LVB fees will be <b>billed by the peak bandwidth</b>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">Daily postpaid</a></td>
</tr></table>


>? You can change the billing mode as instructed in [Changing the Billing Method](https://intl.cloud.tencent.com/document/product/267/30411).  



## Value-added Service Fees

<table>
<tr><th colspan=2 width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td rowspan=2>LVB transcoding</td>
<td>LVB transcoding</td>
<td>
	<li>It can be used in the standard transcoding scenarios of live streaming.</li>
	<li>If the <a href="https://intl.cloud.tencent.com/document/product/267/31064">watermark</a> or <a href="https://intl.cloud.tencent.com/document/product/267/37665">On-Cloud MixTranscoding</a> feature is enabled, standard transcoding fees will be incurred, and the billable resolution will be the resolution of the output live stream.</li>
	<li>The service fees incurred by transcoding are <b>billed by the transcoding duration</b>.</li>
</td>
<td>
	<a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding">Daily postpaid</a>
</td>
</tr><tr>
<td>Top speed codec transcoding</td>
<td>
	<li>It can be used in the top speed codec transcoding scenarios of live streaming.</li>
	<li>If the <a href="https://intl.cloud.tencent.com/document/product/267/31064">watermark</a> or <a href="https://intl.cloud.tencent.com/document/product/267/37665">On-Cloud MixTranscoding</a> feature is enabled, standard transcoding fees will be incurred, and the billable resolution will be the resolution of the output live stream.</li>
	<li>The service fees incurred by transcoding are <b>billed by the transcoding duration</b>.</li></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818#top-speed-codec-transcoding">Daily postpaid</a></td>
</tr><tr>
	<td colspan=2>Global acceleration</td>
	<td>
		<li>Connecting users and global acceleration origin server generates downstream traffic and bandwidth.</li>
		<li>Two billing options are available: bill-by traffic and bill-by-bandwidth.</li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#global-acceleration">Pay-as-you-go daily</a></td>
</tr>
    <tr>
	<td colspan=2>LVB recording</td>
	<td>
		<li>During LVB recording, a recording file is generated based on a recording template and is stored into VOD.</li>
		<li>The services fees incurred by LVB recording are <b>billed by the peak number of concurrent LVB recording channels</b>.</li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-recording">Monthly postpaid</a></td>
</tr><tr>
<td colspan=2>LVB screenshotting</td>
<td>
	<li>During LVB screenshotting, screenshots of a live stream are captured at scheduled time points according to a template and are stored into COS.</li>
	<li>The service fees incurred by screenshotting are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-screencapturing">Monthly postpaid</a></td>
</tr><tr>
	<td colspan=2>Screenshotting and porn detection</td>
	<td>The screenshotting and porn detection features will respectively incur fees.
		<li>The service fees incurred by porn detection are <b>billed by the number of pornographic screenshots detected</b>. The first 1,000 screenshots in every month are free of charge.</li>
		<li>The service fees incurred by screenshotting are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#intelligent-porn-detection">Monthly postpaid</a></td>
</tr><tr>
</tr><tr>
</tr>
</table>



## Extended Service Fees

<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td>Recording storage</td>
<td>Recording files generated by LVB recording need to be stored into VOD, and the incurred service fees are <b>billed by the actual storage duration and data volume</b>. You need to pay for the additional VOD storage fees.</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">contact sales</a></td>
</tr><tr>
<td>Screenshot storage</td>
<td>Screenshot files generated by LVB screenshotting and porn detection need to be stored into COS, and the incurred service fees are <strong>billed by the actual storage duration and data volume</strong>. You need to pay for the additional COS storage fees.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS - pay-as-you-go</a></td>
</tr></table>
