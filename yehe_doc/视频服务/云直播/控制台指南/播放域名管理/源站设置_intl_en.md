If you have a self-built origin server and live streaming source, and want to stream your content through Tencent Cloud, you can configure origin server information for your CSS playback domain name. After the configuration is successful, you can pull live streams from the origin server and distribute them through CSS. This document describes how to configure the origin server.

## Notes
- Origin server configuration takes effect in 1 day.
- After the origin server configuration is enabled, the playback domain name can no longer match the `StreamName` of other push domain names to pull streams, and features such as watermarking, transcoding, recording, screencapture, and porn detection will become unavailable for the domain name. 


## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have built a live streaming origin server.
- You have added a **playback domain**.

## Directions
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the playback domain name to be configured or **Manage** on the right to go to the domain details page.
2. Select **Advanced Configuration**, and click the **Origin Server Settings** tab.
3. Click **Edit** and configure as follows:
 1. Toggle **Origin Server Settings** on.
 2. Select the **Forwarding Protocol** and **Playback Protocol**
 3. Enter an IP or a domain name as the **Master Origin Server Address**.
 4. Click **Save**.

>?**Forwarding Protocol** refers to the protocol supported by CSS when pulling streams from the origin server. **Playback Protocol** refers to the playback protocol used to distribute live content through the CSS CDN.
>- After selecting FLV or RTMP as the forwarding protocol, you can select FLV or HLS as the playback protocol. **If you select FLV as the playback protocol, streams using the RTMP protocol can also be played back.**
>- If the forwarding protocol is HLS, the playback protocol can only be HLS.
>- You can select only one forwarding protocol and multiple playback protocols.


![](https://main.qcloudimg.com/raw/5e085f15c5cd0d09282774f40231301c.png)

