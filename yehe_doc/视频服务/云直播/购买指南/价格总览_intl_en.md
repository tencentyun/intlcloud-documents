>? You can use the [CSS price calculator](https://buy.cloud.tencent.com/price/css/calculator) to estimate your LVB and LEB fees.

Billable items of CSS include basic services and value-added services. You may also incur extended service fees if you use CSS features that rely on the capabilities of other Tencent Cloud products.

![](https://qcloudimg.tencent-cloud.cn/raw/e6890720702b28c1ea9e2a725974b214.png)


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
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818#flow">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>LVB peak bandwidth</td>
<td>
<li/>LVB bandwidth fees are charged based on the downstream and/or upstream bandwidth consumed. By default, only downstream bandwidth is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td><td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/2818#bandwidth">Daily pay-as-you-go</a>
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
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969#flow">Daily pay-as-you-go</a>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>LEB peak bandwidth</td>
<td>
<li/>LEB bandwidth fees are charged based on the downstream and/or upstream bandwidth consumed. By default, only downstream bandwidth is billed.
<li/>Prices differ for regions inside and outside the Chinese mainland.
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969#bandwidth">Daily pay-as-you-go</a>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
</td>
</tr></table>

>! 
>- Because LEB uses channels with ultra-low latency, its traffic/bandwidth fees are slightly higher than those of LVB.
>- CSS provides the monthly billing mode for customers with high demand. To change to monthly billing, please contact your sales rep.
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
<li/>Standard transcoding fees will be incurred if you use the <a href="https://intl.cloud.tencent.com/document/product/267/31064">watermarking</a>, <a href="https://intl.cloud.tencent.com/document/product/267/31071">standard transcoding</a>, or <a href="https://intl.cloud.tencent.com/document/product/267/37665">stream mixing</a> features.
<li/>The fees are based on the <b>transcoding duration</b> and resolution of the output stream.
</ul></td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#n_trans">Daily pay-as-you-go</a></li></ul>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>Top Speed Codec (TSC) transcoding</td>
<td><ul style="margin:0">
<li/>The fees for using the TSC transcoding capability.
<li/>TSC transcoding fees will be incurred if you use the <a href="https://intl.cloud.tencent.com/document/product/267/31071#C_topspeed">TSC transcoding</a> feature.
<li/>The fees are based on the <b>transcoding duration</b> and resolution of the output stream.
</ul><td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#topspeed_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#s_trans">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
<td>Audio transcoding</td>
<td>
<li/>The fees for using the audio transcoding capability.
<li/>Audio transcoding fees will be incurred if you use the <a href="https://intl.cloud.tencent.com/document/product/267/31071#C_audio">audio transcoding</a> or audio mixing feature.
<li/>The fees are based on the <b>audio transcoding duration</b>.
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">Prepaid packages</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#a_trans">Daily pay-as-you-go</a></li>
<li/>Monthly pay-as-you-go
</td>
</tr><tr>
  <td rowspan=2>Live recording</td>
  <td>Recording fees</td>
  <td>The fees are based on the peak number of concurrent recording channels.</td>
<td><a href = "https://intl.cloud.tencent.com/document/product/267/39605">Monthly pay-as-you-go</a></td>
</tr><tr>
  <td>Recording-to-COS fees</td><td>If you record to COS, recording-to-COS fees will be charged based on the recording duration.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605#.E5.BD.95.E5.88.B6.E6.8A.95.E9.80.92-cos-.E6.9C.8D.E5.8A.A1">Monthly pay-as-you-go</a></td>
</tr><tr>
<td rowspan=2>Time shifting</td>
<td>Live streaming traffic</td>
<td>If you create a time shifting template in the CSS console and bind it to a push domain, using the domain for live streaming will incur time shifting fees, which are based on the live streaming traffic.</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/53262">Daily pay-as-you-go</a></td>
</tr><tr>
<td>Total time-shift period</td>
<td>If you have submitted a ticket to enable the time shifting feature, time shifting fees will be based on the total time-shift period.</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/47534">Daily pay-as-you-go</a></td>
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
</tr><tr>
</td>
</tr>
<tr><td rowspan=3>Relay</td>
<td>Relay task duration</td>
<td>Relay fees are billed based on the duration of relay tasks.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059#time">Daily pay-as-you-go</a>
</td>
</tr><tr>
<td>Third-party relaying bandwidth</td>
<td>The fees for relaying to a URL that does not belong to the current Tencent Cloud account.</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059#third_part">Monthly pay-as-you-go</a>
</td>
</tr><tr>
<td>Local mode</td>
<td>Additional fees will be incurred if you enable the local mode for relay.</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/515558">Daily pay-as-you-go</a>
</td>
</tr><tr>
</td>
</tr>
</table>

[](id:extensions)

## Extended Service Fees

<table>
<tr><th width="20%">Billable Item</th><th width="60%">Description</th><th>Billing Mode</th></tr>
<tr>
<td>VOD storage</td>
<td>Saving recording files to VOD will incur VOD storage fees, which are based on the <b>actual storage duration and storage space used</b>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666#media_storage">VOD pay-as-you-go</a></td>
</tr><tr>
<td>COS storage</td>
<td>Saving recording files to COS will incur COS storage fees, which are based on the <b>actual storage duration and storage space used</b>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/40099">COS pay-as-you-go</a></td>
</tr><tr>
<td>Storing screenshots</td>
<td>Screenshots generated by live screencapture and porn detection are saved to COS, which incurs COS storage fees. The fees are billed based on <strong> the actual storage duration and storage space used</strong>.</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS pay-as-you-go</a></td>
</tr></table>
