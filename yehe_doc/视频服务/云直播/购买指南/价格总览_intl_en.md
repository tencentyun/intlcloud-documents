The billable items of LVB include the basic, value-added, and extended service fees, as shown below:

![](https://main.qcloudimg.com/raw/a01e037392642e06335c0967743b5f5f.svg)

- [Basic service fees](#base): incurred by live streaming resource consumption when LVB is used. You can switch between the traffic and peak bandwidth billing modes.
- [Value-added service fees](#appreciation): incurred when value-added features such as LVB transcoding, recording, screenshotting, and porn detection are used. Such features are disabled by default and only incur fees when used.
- [Extended service fees](#extensions): incurred by use of value-added features provided jointly by LVB and other Tencent Cloud services. Each Tencent Cloud service will be charged by its respective billing rule.


## Basic Service Fees
<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td>LVB traffic (default)</td>
<td>If the billing mode is <b>daily bill-by-traffic</b>, the LVB fees will be <strong>billed by the consumed traffic</strong>.</td>
<td><a href="https://cloud.tencent.com/document/product/267/34175#.E6.B5.81.E9.87.8F.E8.AE.A1.E8.B4.B9">Daily postpaid</a></td>
</tr><tr>
<td>LVB bandwidth peak</td>
<td>If the billing mode is <b>daily bill-by-bandwidth</b>, the LVB fees will be <b>billed by the peak bandwidth</b>.</td>
<td><a href="https://cloud.tencent.com/document/product/267/34175#.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9">Daily postpaid</a></td>
</tr></table>


>? You can change the billing mode as instructed in [Changing the Billing Method](https://cloud.tencent.com/document/product/267/32712).  



## Value-added Service Fees

<table>
<tr><th colspan=2 width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td rowspan=2>LVB transcoding</td>
<td>LVB transcoding</td>
<td>
	<li>It can be used in the standard transcoding scenarios of live streaming.</li>
	<li>If the <a href="https://cloud.tencent.com/document/product/267/35253">watermark</a> or <a href="https://cloud.tencent.com/document/product/267/45566">On-Cloud MixTranscoding</a> feature is enabled, standard transcoding fees will be incurred, and the billable resolution will be the resolution of the output live stream.</li>
	<li>The service fees incurred by transcoding are <b>billed by the transcoding duration</b>.</li>
</td>
<td>
	<a href="https://cloud.tencent.com/document/product/267/34175#.E6.A0.87.E5.87.86.E8.BD.AC.E7.A0.81">Daily postpaid</a>
</td>
</tr><tr>
<td>Top speed codec transcoding</td>
<td>
	<li>It can be used in the top speed codec transcoding scenarios of live streaming.</li>
	<li>If the <a href="https://cloud.tencent.com/document/product/267/35253">watermark</a> or <a href="https://cloud.tencent.com/document/product/267/45566">On-Cloud MixTranscoding</a> feature is enabled, standard transcoding fees will be incurred, and the billable resolution will be the resolution of the output live stream.</li>
	<li>The service fees incurred by transcoding are <b>billed by the transcoding duration</b>.</li></td>
<td>
<a href="https://cloud.tencent.com/document/product/267/34175#.E6.9E.81.E9.80.9F.E9.AB.98.E6.B8.85.E8.BD.AC.E7.A0.81">Daily postpaid</a></td>
</tr><tr>
	<td colspan=2>LVB recording</td>
	<td>
		<li>During LVB recording, a recording file is generated based on a recording template and is stored into VOD.</li>
		<li>The services fees incurred by LVB recording are <b>billed by the peak number of concurrent LVB recording channels</b>.</li>
	</td>
<td><a href="https://cloud.tencent.com/document/product/267/34175#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6">Monthly postpaid</a></td>
</tr><tr>
<td colspan=2>LVB screenshotting</td>
<td>
	<li>During LVB screenshotting, screenshots of a live stream are captured at scheduled time points according to a template and are stored into COS.</li>
	<li>The service fees incurred by screenshotting are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://cloud.tencent.com/document/product/267/34175#.E7.9B.B4.E6.92.AD.E6.88.AA.E5.9B.BE">Monthly postpaid</a></td>
</tr><tr>
	<td colspan=2>Screenshotting and porn detection</td>
	<td>The screenshotting and porn detection features will respectively incur fees.
		<li>The service fees incurred by porn detection are <b>billed by the number of pornographic screenshots detected</b>. The first 1,000 screenshots in every month are free of charge.</li>
		<li>The service fees incurred by screenshotting are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://cloud.tencent.com/document/product/267/34175#.E6.99.BA.E8.83.BD.E9.89.B4.E9.BB.84">Monthly postpaid</a></td>
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
<td><a href="https://cloud.tencent.com/document/product/266/14667#1.-.E5.AD.98.E5.82.A8.E8.B5.84.E6.BA.90.E5.8C.85">VOD - pay-as-you-go</a></td>
</tr><tr>
<td>Screenshot storage</td>
<td>Screenshot files generated by LVB screenshotting and porn detection need to be stored into COS, and the incurred service fees are <strong>billed by the actual storage duration and data volume</strong>. You need to pay for the additional COS storage fees.</td>
<td><a href="https://cloud.tencent.com/document/product/436/36522">COS - pay-as-you-go</a></td>
</tr></table>