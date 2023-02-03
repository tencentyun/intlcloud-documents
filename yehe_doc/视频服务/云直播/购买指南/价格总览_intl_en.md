>? You can use the [CSS price calculator](https://buy.cloud.tencent.com/price/css/calculator) to estimate your LVB and LEB fees.

Billable items of CSS include basic services and value-added services. You may also incur extended service fees if you use CSS features that rely on the capabilities of other Tencent Cloud products.

![](https://qcloudimg.tencent-cloud.cn/raw/7970d2961c95cd19a4e7568f3ea60467.png)


- [Basic service fees](#base) are the fees for using LVB and LEB and are charged based on either traffic or peak bandwidth usage.
- [Value-added service fees](#appreciation) are the fees for using value-added features such as transcoding, recording, time shifting, screencapture, porn detection, and relay. These features are disabled by default and are billed only when enabled.
- [Extended service fees](#extensions) are the fees for using the capabilities of other Tencent Cloud products and are charged according to the billing rules of the corresponding products.

[](id:base)
## Basic Service Fees

Basic service fees include LVB fees and LEB fees.

<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Billing Mode</th></tr>
<tr>
<td>LVB traffic<br>(default)</td>
<td>
<li/>LVB traffic fees are charged based on the downstream and/or upstream traffic consumed. By default, only downstream traffic is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>LVB peak bandwidth</td>
<td>
<li/>LVB bandwidth fees are charged based on the downstream and/or upstream bandwidth consumed. By default, only downstream bandwidth is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>LEB traffic<br>(default)</td>
<td>
<li/>LEB traffic fees are charged based on the downstream and/or upstream traffic consumed. By default, only downstream traffic is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td>
<td>
<li/><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">Prepaid packages</a>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39969">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>LEB peak bandwidth</td>
<td>
<li/>LEB bandwidth fees are charged based on the downstream and/or upstream bandwidth consumed. By default, only downstream bandwidth is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39969">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr></table>

>! 
>- Because LEB uses channels with ultra-low latency, its traffic/bandwidth fees are slightly higher than those of LVB.
>- CSS provides monthly billing mode for customers with high demand. To change to monthly billing, please contact your sales rep.
>- For more information about billing modes, see [Changing Billing Modes](https://intl.cloud.tencent.com/document/product/267/30411).  


[](id:appreciation)
## Value-Added Service Fees

<table>
<tr><th colspan=2 width="20%">Billable Item</th><th width="60%">Description</th><th>Billing Mode</th></tr>
<tr>
<td rowspan=3>Live transcoding</td>
<td>Standard transcoding</td>
<td><ul style="margin:0">
<li/>The fees for using the standard transcoding capability.
<li/>You will incur standard transcoding fees for using the <a href="https://intl.cloud.tencent.com/document/product/267/31064">watermarking</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">standard transcoding</a>, or <a href="https://intl.cloud.tencent.com/document/product/267/37665">stream mixing</a> features.
<li/>The fees are based on the <b>transcoding duration</b> and resolution of the output stream.
</ul></td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">Prepaid packages</a></li>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Daily pay-as-you-go</a></li></ul>
	<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>Top Speed Codec (TSC) transcoding</td>
<td><ul style="margin:0">
<li/>The fees for using the TSC transcoding capability.
<li/>You will incur TSC transcoding fees for using the <a href="https://intl.cloud.tencent.com/document/product/267/31071">TSC transcoding</a> feature.
<li/>The fees are based on the <b>transcoding duration</b> and resolution of the output stream.
</ul><td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#topspeed_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>Audio transcoding</td>
<td>
<li/>The fees for using the audio transcoding capability.
<li/>You will incur audio transcoding fees for using <a href="https://intl.cloud.tencent.com/document/product/267/31071">audio transcoding</a> and audio mixing.
<li/>The fees are based on the <b>audio transcoding duration</b>.
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
  <td colspan=2>Live recording</td>
  <td>
    <li>Audio and video are recorded according to a recording template and the recording files generated are saved to VOD.</li>
    <li>Recording fees are based on the <b>peak number of concurrent recording channels</b>.</li>
  </td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39605">Monthly pay-as-you-go</a></td>
</tr><tr>
<td colspan=2>Time shifting</td>
<td>Time shifting fees are based on the total time-shift period.</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/47534">Daily pay-as-you-go</a>
</tr><tr>
<td colspan=2>Live screencapture</td>
<td>
  <li>Screenshots of a live stream are taken at times specified in a template and saved to COS.</li>
  <li>Screencapture is billed based on <b>the number of screenshots taken</b>. We offer a free tier of 1,000 screenshots per month.</li>
</td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39606">Monthly pay-as-you-go</a></td>
</tr><tr>
  <td colspan=2>Intelligent porn detection</td>
  <td>Using the porn detection feature will incur screencapture and porn detection fees.
    <li>Porn detection is billed based on <b>the number of screenshots analyzed.</b> We offer a free tier of 1,000 screenshots for porn detection per month.</li>
    <li>Screencapture is billed based on <b>the number of screenshots taken</b>. We offer a free tier of 1,000 screenshots per month.</li>
</td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39607">Monthly pay-as-you-go</a></td>
</tr>
<tr><td colspan=2>Pull and relay</td>
<td>Relay fees are billed based on the duration of pull and relay tasks.</td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059">Daily pay-as-you-go</a></li>
</td>
</tr><tr>
<td colspan=2>Pull and relay to third parties</td>
<td>The fees for relaying to a URL that does not belong to the current Tencent Cloud account.</td>
<td>
<a href = "https://intl.cloud.tencent.com/document/product/267/41059">Monthly pay-as-you-go</a>
</td>
</tr>
</table>

[](id:extensions)
## Extended Service Fees

<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Billing Mode</th></tr>
<tr>
<td>Storing recording files</td>
<td>Recording files are saved to VOD, which incurs VOD storage fees. The fees are based on <b>the actual storage duration and storage space used</strong>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666">VOD pay-as-you-go</a></td>
</tr><tr>
<td>Storing screenshots</td>
<td>Screenshots generated by live screencapture and porn detection are saved to COS, which incurs COS storage fees. The fees are billed based on <strong> the actual storage duration and storage space used</strong>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS pay-as-you-go</a></td>
</tr></table>