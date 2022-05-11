Before using CSS, you need to know the following use limits:

<table>
<tr><th>Item</th><th>Description</th></tr>
<tr>
<td>CSS domain name</td>
<td><ul style="margin:0">
 <li>Multiple playback and push domain names can be created under an account. If the acceleration region of a domain name is the Chinese mainland or global, the domain name must have an ICP filing from MIIT, and the filing information must be currently valid and available.</li>
    <li>You can manage up to 100 domain names under one account by default. If your business scale is large, you can <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to apply for increasing the maximum number of domain names.</li>
    <li>We recommend you keep the length of a domain name no more than 45 characters. If you want a <strong>longer</strong> domain name, you need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.</li>
<li>A domain name managed by CSS can be used to push or play back live streams normally only after the domain name is resolved. For more information, see <a href="https://intl.cloud.tencent.com/document/product/267/31057">Configuring CNAME for Domain Name</a>.</li></ul></td>
</tr><tr>
<td>Live push</td>
<td>The CSS service does not limit the push bitrate and supports common resolutions and corresponding bitrates. To avoid push lag, we recommend you keep the bitrate below 4 Mbps.</td>
</tr><tr>
<td>Live playback</td>
<td><ul style="margin:0">
	<li>A stream can be played back only when the `StreamName` of the playback address is the same as that of the push address.</li>
	<li>There is no limit to the number of live stream viewers. You can set your own bandwidth limit for live streaming.</li>
	<li/>If you need additional support for a large-scale surge in live streaming traffic, you need to submit a ticket or contact your Tencent Cloud rep three business days in advance for assistance. Such surges mainly include the following two types:<ul style="margin:0">
		<li/>The sudden daily peak bandwidth exceeds 200 Gbps, and the surge is 200% of the daily peak.
		<li/>The sudden daily peak bandwidth exceeds 500 Gbps.
	</ul>
</ul></td>
</tr><tr>
<td>Template configuration</td>
<td>After a template is successfully bound, it takes 5–10 minutes for it to take effect.</td>
</tr><tr>
<td>Daily billing mode switch</td>
<td>You can select bill-by-traffic or bill-by-bandwidth for daily billing. You can switch the billing mode only once per day, and the switch will take effect on the next day.</td>
</tr><tr>
<td>Supported push protocols</td>
<td>CSS supports the RTMP and SRT protocols. For more information, see <a href="https://intl.cloud.tencent.com/document/product/267/7968">Live Streaming Basics</a>.</td>
</tr><tr>
<td>Supported playback protocols</td>
<td><ul style="margin:0">
	<li>CSS supports the RTMP, FLV, and HLS playback protocols. For more information, see <a href="https://intl.cloud.tencent.com/document/product/267/7968">Live Streaming Basics</a>.</li>
	<li>LEB supports the WebRTC playback protocol.</li>
</ul></td>
</tr></table>


