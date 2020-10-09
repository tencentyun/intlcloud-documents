### Prerequisites
- You have signed up for a Tencent Cloud account and activated the [LVB service](https://intl.cloud.tencent.com/product/LVB).
- You have your own domain name.
- You have added push/playback domain names in the **LVB Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and successfully configured the CNAME record. For detailed directions, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/267/35970).

<span id="push"></span>
### Splicing Push URLs
During actual service use, if there are many live rooms, you will not be able to manually create push and playback URLs for each host. In this case, you can **splice** such addresses on the server. Any URL that meets Tencent Cloud standards can be used for push. A standard push URL consists of four parts, as shown below:
![](https://main.qcloudimg.com/raw/679602c838e8dfd3b61acefebb221d13.jpg)

- **Domain**
Push domain name, which can be the default push domain name provided by Tencent Cloud LVB or your own push domain name with a successfully configured CNAME record.
- **AppName**
LVB application name, which is `live` by default and customizable.
- **StreamName (stream ID)**
Custom stream name and unique ID of a live stream. We recommend you use a random numerical or alphanumerical string.
- **Authentication key (optional)**
It consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If push authentication is enabled, the URL used for push should contain the authentication key. If push authentication has not been enabled, the URL used for push does not need to contain "?" and the content following it.
 - **txTime (address expiration time)** 
It indicates the time when the URL expires, which is expressed as a hexadecimal Unix timestamp.
	
	>?For example, `5867D600` indicates that the URL will expire at 00:00:00, January 1, 2017. Generally, `txTime` is set to 24 hours later. The expiration time should be neither too early nor too late. If it is too early, when the host encounters network jitters during live streaming, the push will not be resumed because the push URL will have expired.
 - **txSecret (hotlink protection signature)**
It is used to prevent attackers from forging your backend to generate push URLs. For more information on the calculation method, please see [Best Practices - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

<span id="play"></span>
### Splicing Playback URLs
A playback address is mainly composed of the playback prefix, playback domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication parameter, and other custom parameters, as shown below:	

```	
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time) 	
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)	
```

- **Playback prefix**	
<table>
    <tr><th>Playback Protocol</th><th>Playback Prefix</th><th>Notes</th></tr>
    <tr>
        <td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>We do not recommend RTMP as it has poor instant streaming performance and does not support high concurrence.</td>
    </tr><tr>
        <td>HTTP-FLV</td>
				<td><code>http://</code> or <code>https://</code></td>
        <td>We recommend HTTP-FLV as it has good instant streaming performance and supports high concurrence.</td>
    </tr><tr>
        <td>HLS (M3U8)</td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>We recommend HLS for mobile users and for the Safari browser on macOS.</td>
    </tr>
</table>
- **Domain**	
	Playback domain name, which should be your own domain name with a successfully configured CNAME record.
- **AppName**	
  LVB application name used to identify the storage path of a live streaming media file. The LVB application name is `live` by default and customizable.
- **StreamName (stream name)<span id="streamname"></span>**	
  Custom stream name and unique ID of a live stream. We recommend you use a random numerical or alphanumerical string.
- **Authentication parameters (optional)**	
	It consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`.
If playback authentication is enabled, the URL used for playback should contain the authentication key. If playback authentication has not been enabled, the URL used for playback does not need to contain "?" and the content following it.
 - **txTime (address validity period):** indicates the time when the URL expires, which is expressed as a hexadecimal Unix timestamp.
 - **txSecret (hotlink protection signature):** used to prevent attackers from forging your backend to generate playback URLs. For more information on the calculation method, please see [Best Practices - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).


<span id="push_code"></span>
### Viewing Sample Push Codes
Go to the **LVB Console** > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select a pre-configured push domain name, and click **Manage** > **Push Configuration** to display the **Push Address Sample Code** (for both PHP and Java) that demonstrates how to generate a hotlink protection address. For detailed directions, please see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).

