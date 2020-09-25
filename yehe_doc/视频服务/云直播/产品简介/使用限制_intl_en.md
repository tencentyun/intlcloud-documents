Before using LVB, you need to know the following use limits:

<table>
<tr><th>Item</th><th>Description</th></tr>
<tr>
<td>LVB domain name</td>
<td><ul style="margin:0">
<li>Multiple playback and push domain names can be created under an account by default. If a domain name is used in Mainland China, it must have an ICP filing from the MIIT, and the current filing information must be normal and available.</li><li>We recommend you use a domain name containing up to 30 characters. If it has over <strong>30</strong> characters, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.</li>
<li>A domain name managed by LVB can be used to push or play back live streams normally only after being resolved. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/31057">Configuring CNAME for Domain Name</a>.</li></td>
</tr><tr>
<td>LVB push</td>
<td>The LVB service does not limit the push bitrate and supports common resolutions and corresponding bitrates. To avoid push lag, we recommend you keep the bitrate below 4 Mbps.</td>
</tr><tr>
<td>LVB playback</td>
<td><ul style="margin:0">
<li>Only when the `StreamName` of the playback address is the same as that of the push address can the corresponding stream be played back.</li><li>The number of live streaming viewers is not limited, and you can set a bandwidth limit.</li></td>
</tr><tr>
<td>Template configuration</td>
<td>After the association with a template is successfully configured, it will take effect in 5–10 minutes.</td>
</tr><tr>
<td>Daily billing mode switch</td>
<td>You can select bill-by-traffic or bill-by-bandwidth for daily billing, and you can switch the billing mode only once per day (the switch will take effect on the next day).</td>
</tr><tr>
<td>Supported push protocols</td>
<td>LVB supports the RTMP and SRT output protocols. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/7968">Basic LVB Features</a>.</td>
</tr><tr>
<td>Supported playback protocols</td>
<td><ul style="margin:0">
<li>LVB supports the RTMP, FLV, and HLS playback protocols. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/267/7968">Basic LVB Features</a>.</li>
<li>LEB supports the WebRTC playback protocol.</li>
<li>Playback of a pulled stream supports a bandwidth of up to 200 Gbps. If you need a higher bandwidth, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> or contact your Tencent Cloud rep for assistance.</li></td>
</tr><tr>
<td>Live director</td>
<td><ul style="margin:0">
<li>You can create up to <b>three</b> live director instances under one account. If there are already three instances, only after an existing instance is deleted can a new one be added. To add more instances, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li>
<li>You can add up to five VOD files to the VOD input playback list.</li>
<li>Third-party relayed push supports up to three streams, one of which is relayed to the current LVB account by default, and the other two can be relayed to third-party vendors.</li></td>
</tr></table>
