If you have a self-built origin server and live streaming source, and you want to stream your content through Tencent Cloud, you can configure origin server information for your CSS playback domain name. After the configuration is successful, you can pull live streams from the origin server and distribute them through CSS. This document describes how to configure the origin server.

## Notes
- Origin server configuration takes effect about one hour after configuration is complete.
- After configuring an origin server for a playback domain, you can no longer bind a push domain to the playback domain by specifying a `StreamName`. Nor can you configure watermarking, transcoding, recording, screenshot, or porn detection tasks for the playback domain. 


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have built a live streaming origin server.
- You have added a **playback domain name**.

## Directions
1. In the CSS console, select [Domain Management](https://console.cloud.tencent.com/live/domainmanage) on the left sidebar. Click the name of your playback domain or click **Manage** on the right.
2. Select the **Advanced Configuration** tab.
3. In the **Origin server settings** area, click **Edit** and follow the steps below:
 1. Toggle on **Origin server settings**.
 2. Complete the settings as follows.
<table id="setmess">
<tr><th width="14%">Configuration Item</th><th>Description</th>
</tr><tr>
<td>Primary origin server</td>
<td>You can either specify an <b>origin server IP</b> or <b>origin server domain</b>:
<ul style="margin:0">
<li>If you select “Origin server IP”, you need to enter the IP address of your origin server and the port number.</li>
<li>If you select “Origin server domain”, you need to enter the domain name of your origin server and the port number.</li>
</ul></td>
</tr><tr>
<td>Backup origin server</td>
<td><ul style="margin:0">You can configure only one backup origin server. Whether you enter an IP or domain name here depends on whether you have specified an IP or domain for the primary origin server. The port number of the backup origin server is the same as that of the primary.
</ul></td>
</tr><tr>
<td>Forwarding protocol</td>
<td><ul style="margin:0">
<li>RTMP, FLV, and HLS are supported.</li>
<li>For HLS, you can enable HTTP header pass-through and parameter pass-through.</li>
</ul></td>
</tr><tr>
<td>Timeout and retry</td>
<td><ul style="margin:0">The timeout period cannot be longer than 60,000 milliseconds; the value range for maximum retry attempts is 1-10.
</ul></td>
</tr><tr>
<td>Playback protocol</td>
<td><ul style="margin:0">
<li>If the forwarding protocol is RTMP, RTMP is supported for playback by default. You can also select FLV and HLS.</li>
<li>If the forwarding protocol is FLV, FLV is supported for playback by default. You can also select HLS.</li>
<li>If the forwarding protocol is HLS, the playback protocol must also be HLS.</li></ul></td>
</tr><tr>
<td>Index buffer size</td>
<td><ul style="margin:0">If you select HLS as the forwarding protocol, you can specify the index buffer size (milliseconds). Value range: 1,000-60,000.
</ul></td>
</tr><tr>
<td>Segment size</td>
<td><ul style="margin:0">If you select HLS as the forwarding protocol, you can specify the segment size (milliseconds). Value range: 1,000-60,000.
</ul></td>
</tr></table>

 4. Click **Save**.
>? **Forwarding protocol** refers to the protocol supported by CSS when pulling streams from the origin server. **Playback protocol** refers to the protocol used to distribute live content through the CSS CDN.

![](https://qcloudimg.tencent-cloud.cn/raw/bc6843d5eca8e81b07931b7ea44aceba.png) 
