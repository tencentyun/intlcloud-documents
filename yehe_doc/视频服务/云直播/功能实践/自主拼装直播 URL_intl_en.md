## Notes
After you create a [transcoding template](https://intl.cloud.tencent.com/document/product/267/31071) and [bind](https://intl.cloud.tencent.com/document/product/267/31071#related) it with a playback domain name, you need to add the transcoding template name after the `StreamName` of the live stream with the transcoding configuration in the format of `StreamName_transcoding template name`. For details, see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

## Prerequisites
- You have signed up for a Tencent Cloud account and activated the [CSS service](https://intl.cloud.tencent.com/product/css).
- You have applied for a domain name through [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns).
- You have added push/playback domain names in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** of the CSS console and successfully configured the CNAME record. For detailed directions, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/267/35970).

[](id:push)
## Splicing Push URLs
If you run a large number of live streaming rooms, it is impossible to manually generate a push and playback URL for each host. In such cases, you can use the server to automatically **splice** the addresses. Any URL that meets Tencent Cloud standards can be used for push. A standard push URL consists of four parts, as shown below:
![](https://main.qcloudimg.com/raw/095b7c120b62ac8a171603d4fff67cb2.png)
- **Domain**
Push domain name, which can be the default push domain name provided by Tencent Cloud CSS or a push domain name that you have added and created a CNAME record for.
- **AppName**
Live streaming application name, which is `live` by default and is customizable.
- **StreamName (stream ID)**
Custom stream name, which is the unique ID of a live stream. We recommend that you use a random numeric or alphanumeric string for this parameter.
- **Authentication key (optional)**
An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If push authentication is enabled, the URL used for push must contain an authentication key. If push authentication is disabled, the push URL does not need to contain "?" and the content following it.
 - **txTime (URL expiration time)** 
The time when the URL expires, in the format of hexadecimal Unix timestamp.
  >?For example, `5867D600` means that the URL expires at 00:00:00, January 1, 2017. The validity period should neither be too short nor too long. Most of our clients set `txTime` to a point 24 hours or longer from the current time. If the validity period is too short, after a host is disconnected due to network problems during a live broadcast, it may be impossible to resume the push due to expiration of the push URL.
 - **txSecret (hotlink protection signature)**
The `txSecret` signature serves to prevent attackers from forging a backend to generate push URLs. For the calculation method, see [Best Practice - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

[](id:play)
## Splicing Playback URLs
A playback URL consists of a playback protocol prefix, domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication key, and other custom parameters. Below are a few examples. 

``` 
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

- **Playback prefix**  
<table>
    <tr><th>Playback Protocol</th><th>Playback Prefix</th><th>Notes</th></tr>
		<tr>
        <td>WebRTC</td>
        <td><code>webrtc://</code> </td>
        <td>We recommend WebRTC most as it has the best instant streaming performance and supports ultra-high concurrency.</td>
    </tr><tr>
        <td>HTTP-FLV </td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>We recommend HTTP-FLV as it has good instant streaming performance and supports high concurrency.</td>
    </tr><tr>
				<td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>We do not recommend RTMP as it has poor instant streaming performance and does not support high concurrency.</td>
    </tr><tr>
        <td>HLS (M3U8)</td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>We recommend HLS for mobile clients and for the Safari browser on macOS.</td>
    </tr>
</table>
- **Domain**  
  Playback domain name, a domain name you have added and created a CNAME record for.
- **AppName** 
  Live streaming application name used to identify the storage path of a live streaming media file. The application name is `live` by default and customizable.
- **StreamName (stream name)[](id:streamname)**  
  Custom stream name, which is the unique ID of a live stream. We recommend you use a random numerical or alphanumerical string.
- **Authentication key (optional)** 
  An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If playback authentication is enabled, the URL used for playback must contain an authentication key. If it is disabled, the playback URL does not need to contain "?" and the content following it.
 - **txTime (address expiration time):** the time when the URL expires, in the format of hexadecimal Unix timestamp.
 - **txSecret (hotlink protection signature):** it serves to prevent attackers from forging a backend to generate playback URLs. For the calculation method, see [Best Practice - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).


[](id:push_code)
## Viewing Sample Push Codes
Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** of the CSS console, select a pre-configured push domain name, and click **Manage** > **Push Configuration** to display the **Push Address Sample Code** (for both PHP and Java) that demonstrates how to generate a hotlink protection address. For detailed directions, please see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).


