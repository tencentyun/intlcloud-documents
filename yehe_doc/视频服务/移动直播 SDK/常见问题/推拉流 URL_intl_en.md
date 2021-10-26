### Prerequisites
- You have signed up for a Tencent Cloud account and activated the [CSS service](https://intl.cloud.tencent.com/product/css).
- You have applied for a domain name at [Tencent Cloud Domain Service](https://dnspod.cloud.tencent.com/?from=qcloudProductDns).
- You have added publishing/playback domain names in the CSS console > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**. For detailed directions, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).
- You have [configured CNAME](https://intl.cloud.tencent.com/document/product/267/31057) for your domain names.

[](id:manual)
### Generating live streaming URLs in the console  
1. Log in to the CSS console.  
2. Go to **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator), and do the following:
  1. Select a domain type.
  2. Select the domain name you have added in **Domain Management**.
  3. Enter a custom `AppName` value (`live` by default). `AppName` is used to differentiate the paths of applications under the same domain name.
  4. Enter a custom `StreamName` value.
  5. Select an expiration time for the address.
6. Click **Generate Address** to generate your publishing/playback address.
>? 
>- `AppName` is a custom value and can contain only letters, numbers, and special characters.
>- Here is another way to generate publishing addresses: In **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, find the publishing domain name you want use to generate a publishing address, click **Manage**, select **Push Configuration**, enter an expiration time for the address and a custom `StreamName value`, and click **Generate Push Address**.

[](id:example)
### Viewing the sample code of publishing URLs
Go to [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage) of the CSS console, find the publishing domain name you created, click **Manage**, and select **Push Configuration**. Scroll down and you will find **Push Address Sample Code** (for PHP and Java). The code demonstrates how to generate a hotlink protection address. For detailed directions, see [Push Configuration](https://intl.cloud.tencent.com/document/product/267/31059).

[](id:assemble_push)[](id:push)
### Splicing publishing URLs
If you run a large number of live streaming rooms, it is impossible to manually generate a publishing and playback URL for each host. In such cases, you can use the server to **automatically splice** the URLs. Any URL that meets Tencent Cloud standards can be used for publishing. A standard publishing URL consists of four parts, as shown below:
![](https://main.qcloudimg.com/raw/c2ea59c7bd0d42c729e67dea5ec73e9d.png)

- **Domain**
Domain name for publishing, which can be the default publishing domain name provided by Tencent Cloud CSS or a publishing domain name that you have added and created a CNAME record for
- **AppName**
Application name, which is a custom value and `live` by default
- **StreamName (stream ID)**
Custom stream name, which is the unique ID of a live stream. We recommend that you use a random numeric or alphanumeric string for this parameter.
- **Authentication key (optional)**
An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)`.
If publishing authentication is enabled, the URL used for publishing must contain an authentication key. If publishing authentication is disabled, the publishing URL ends before “?”.
 - **txTime (URL expiration time)** 
The time when the URL expires, in the format of hexadecimal Unix timestamp
>?For example, `5867D600` means that the URL expires at 00:00:00, January 1, 2017. The validity period should neither be too short nor too long. Most of our clients set `txTime` to a point 24 hours or longer from the current time. If the validity period is too short, if a host is disconnected during a live stream, he or she may be unable to resume publishing due to the expiration of the publishing URL.
 - **txSecret (hotlink protection signature)**
`txSecret` can prevent attackers from forging your backend to generate publishing URLs. For the calculation method, see [Best Practice > Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

[](id:assemble_play)[](id:play)
### Splicing playback URLs
A playback URL consists of a playback protocol prefix, domain name (`domain`), application name (`AppName`), stream name (`StreamName`), playback protocol suffix, authentication key, and other custom parameters. Below are a few examples. 

``` 
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)
http://domain/AppName/StreamName.flv?txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)
```

- **Prefix**  
<table>
    <tr><th>Playback Protocol</th><th>Playback Prefix</th><th>Notes</th></tr>
<tr>
        <td>WebRTC</td>
        <td><code>webrtc://</code> </td>
        <td>Strongly recommended; best instant streaming performance; ultra-high concurrency</td>
    </tr><tr>
        <td>HTTP-FLV </td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>Recommended, excellent instant streaming performance; high concurrency</td>
    </tr><tr>
<td>RTMP</td>
        <td><code>rtmp://</code> </td>
        <td>Not recommend; poor instant streaming performance; unable to handle high concurrency</td>
    </tr><tr>
        <td>HLS (M3U8)</td>
        <td><code>http://</code> or <code>https://</code></td>
        <td>We recommend HLS for mobile clients and for the Safari browser on macOS.</td>
    </tr>
</table>
- **Domain**  
  Domain name for playback, which must be a domain you have added and created a CNAME record for
- **AppName** 
  Application name, which is a custom value (`live` by default) that identifies the storage path of a live streaming media file
- **StreamName (stream name)**  [](id:streamname)
  Custom stream name, which is the unique ID of a live stream. We recommend that you use a random numeric or alphanumeric string for this parameter.
- **Authentication key (optional)** 
  An authentication key consists of `txSecret` and `txTime`: `txSecret=Md5(key+StreamName+hex(time))&amp;txTime=hex(time)`.
If playback authentication is enabled, the URL used for playback must contain an authentication key. If it is disabled, the playback URL does not need to contain "?" and the content following it.
 - **txTime (address expiration time):** the time when the URL expires, in the format of hexadecimal Unix timestamp
 - **txSecret (hotlink protection signature):** a signature that prevents attackers from forging your backend to generate playback URLs. For the calculation method, see [Best Practice > Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).

[](id:rtc)
### Splicing URLs for RTC-based mic connect/host competition
You need to splice publishing and playback URLs for RTC-based [mic connect](https://intl.cloud.tencent.com/document/product/1071/39888) and [host competition](https://intl.cloud.tencent.com/document/product/1071/42323#step1).

- **Publishing URL**[](id:rtc_push)
You need to splice a publishing URL by yourself in your project code. The format is as shown below.
```http
trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx
```
	The table below lists the key fields in a publishing URL and their meanings.
<table>
<tr><th>Field</th><th>Description</th></tr><tr>
<td>trtc://</td>
<td>Prefix of a publishing URL for interactive live streaming</td>
</tr><tr>
<td>cloud.tencent.com</td>
<td>Dedicated domain name for interactive live streaming, <b>which you must not modify</b></td>
</tr><tr>
<td>push</td>
<td>Identifier, which indicates publishing</td>
</tr><tr>
<td>streamid</td>
<td>Stream ID, which is a custom value specified by yourself</td>
</tr><tr>
<td>sdkappid</td>
<td>The `SDKAppID` generated in “Activate TRTC”</td>
</tr><tr>
<td>userId</td>
<td>User ID of the host, which is a custom value specified by yourself</td>
</tr><tr>
<td>usersig</td>
<td>User signature calculated from the key obtained in “Activate TRTC”</td>
</tr></table>
- **Playback URL**[](id:rtc_play)
You need to splice a playback URL by yourself in your project code. The format is as shown below.
```http
trtc://cloud.tencent.com/play/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx
```
	The table below lists the key fields in a playback URL and their meanings.
<table>
<tr><th>Field</th><th>Description</th></tr>
<tr>
<td>trtc://</td>
<td>Prefix of a playback URL for interactive live streaming</td>
</tr><tr>
<td>cloud.tencent.com</td>
<td>Dedicated domain name for interactive live streaming, <b>which you must not modify</b></td>
</tr><tr>
<td>play</td>
<td>Identifier, which indicates playback</td>
</tr><tr>
<td>streamid</td>
<td>Stream ID, which is a custom value specified by yourself</td>
</tr><tr>
<td>sdkappid</td>
<td>The `SDKAppID` generated in “Activate TRTC”</td>
</tr><tr>
<td>userId</td>
<td>User ID of the host, which is a custom value specified by yourself</td>
</tr><tr>
<td>usersig</td>
<td>User signature calculated from the key obtained in “Activate TRTC”</td>
</tr></table>
