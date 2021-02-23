>? You can [CSS Price Calculator](https://buy.cloud.tencent.com/pricing/css/calculator) to receive an estimate of your LVB costs.

The billable items of LVB include the basic, value-added, and extended service fees, as shown below:

![](https://main.qcloudimg.com/raw/fdf794a99893c09a002b3bea848b3238.png)


- [Basic service fees](#base): incurred by live streaming resource consumption when LVB is used. You can switch between the traffic and peak bandwidth billing modes.
- [Value-added service fees](#appreciation): incurred when value-added features such as LVB transcoding, recording, screencapturing, and porn detection are used. Such features are disabled by default and only incur fees when used.
- [Extended service fees](#extensions): incurred when value-added features provided jointly by LVB and other Tencent Cloud services are used. Each Tencent Cloud service will be charged according to its respective billing rules.

[](id:base)

## Basic Service Fees
<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td>LVB traffic (default)</td>
<td>If the billing mode is <b>daily bill-by-traffic</b>, the LVB fees will be <strong>billed by the consumed traffic</strong>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic">Daily pay-as-you-go</a></td>
</tr><tr>
<td>LVB peak bandwidth</td>
<td>If the billing mode is <b>daily bill-by-bandwidth</b>, the LVB fees will be <b>billed by the peak bandwidth</b>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#bill-by-bandwidth">Daily pay-as-you-go</a></td>
</tr></table>

>! You can change your billing mode as instructed in [Changing Billing Methods](https://intl.cloud.tencent.com/document/product/267/30411).  


[](id:appreciation)

## Value-Added Service Fees

<table>
<tr><th colspan=2 width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td rowspan=3>LVB transcoding</td>
<td>Standard transcoding</td>
<td><ul style="margin:0">
<li/>Using LVB standard transcoding will incur fees.
<li/>The standard transcoding fees will be incurred when <a href="https://intl.cloud.tencent.com/document/product/267/31064">watermarking</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071#C_trans">standard transcoding</a>, or <a href="https://intl.cloud.tencent.com/document/product/267/37665">stream mix</a> is used during live streaming.
<li/>The fees are billed by <b>the transcoding duration</b> according to the billing tier of the output live stream image dimensions.
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604#n_trans">Daily pay-as-you-go</a></li></ul>
</td>
</tr><tr>
<td>Top speed codec transcoding</td>
<td><ul style="margin:0">
<li/>Using LVB top speed codec transcoding will incur fees.
<li/>The top speed codec transcoding fees will be incurred when <a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-top-speed-codec-transcoding-template">top speed codec transcoding</a> is used.
<li/>The fees are billed by <b>the transcoding duration</b> according to the billing tier of the output live stream image dimensions.
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#s_trans">Daily pay-as-you-go</a></li></td>
</tr><tr>
<td>Audio transcoding</td>
<td>
<li/>Using LVB audio transcoding will incur fees.
<li/>The audio transcoding fees will be charged when <a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-pure-audio-transcoding-template">audio transcoding</a>, audio stream mix, or audio/video stream separation is used.
<li/>The fees are billed by <b>the audio transcoding duration</b>.
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#a_trans">Daily pay-as-you-go</a></li></td>
</tr><tr>
  <td colspan=2>LVB recording</td>
  <td>
    <li>During LVB recording, a recording file is generated based on a recording template and is stored into VOD.</li>
    <li>The services fees incurred by LVB recording are <b>billed by the peak number of concurrent LVB recording channels</b>.</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">Monthly postpaid</a></td>
</tr><tr>
<td colspan=2>LVB screencapturing</td>
<td>
  <li>During LVB screencapturing, screenshots of a live stream are captured at scheduled time points according to a template and stored into COS.</li>
  <li>The service fees incurred by screencapturing are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">Monthly postpaid</a></td>
</tr><tr>
  <td colspan=2>Intelligent porn detection</td>
  <td>The screencapturing and porn detection features will incur fees separately.
    <li>The service fees incurred by porn detection are <b>billed by the number of pornographic screenshots detected</b>. The first 1,000 screenshots in every month are free of charge.</li>
    <li>The service fees incurred by screencapturing are <b>billed by the number of screenshots</b>. The first 1,000 screenshots in every month are free of charge.</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">Monthly postpaid</a></td>
</tr><tr>
</tr>
</table>
 


[](id:extensions)

## Extended Service Fees

<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Payment Mode</th></tr>
<tr>
<td>Recording storage</td>
<td>Recording files generated by LVB recording need to be stored into VOD, and the incurred service fees are <b>billed by the actual storage duration and data volume</b>. You also need to pay for the VOD storage fees.</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">Contact sales</a></td>
</tr><tr>
<td>Screenshot storage</td>
<td>Screenshot files generated by LVB screencapturing and porn detection need to be stored into COS, and the incurred service fees are <strong>billed by the actual storage duration and data volume</strong>. You also need to pay for the COS storage fees.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS pay-as-you-go</a></td>
</tr></table>
