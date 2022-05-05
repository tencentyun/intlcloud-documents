Live screencapture takes real-time screenshots from a live stream at the specified interval and stores them in COS. A screencapture callback returns information about stored screenshots, including the screenshot generation time, image size, file path, and download link. To receive screencapture callbacks, you need to configure your server address in a callback template and bind the template with your push domain. When a live screencapture event occurs, the CSS backend will send the screenshot information to the server configured.

This document describes the fields in a live screencapture callback message.

## Notes

- This document assumes you already know how to configure and [receive](https://intl.cloud.tencent.com/document/product/267/38080) callbacks.
- The information returned by a screencapture callback can be used for porn detection, live video thumbnail generation, and other scenarios.

## Screencapture Event Parameters
### Event type

| Event Type | Value           |
| :------- | :------------- |
| Live screencapture | event_type = 200 |

### Common callback parameters
<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default validity period of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, then this notification is considered invalid, thereby preventing network replay attacks. <li>The value of `t` is a decimal Unix timestamp, that is, the number of seconds that have elapsed since 00:00:00 (UTC/GMT time), January 1, 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Security signature. sign = MD5(key + t). <br>Tencent Cloud splices the encryption <a href="#key">key</a> and `t`, generates the MD5 hash of the spliced string, and embeds it in callback messages. Your backend server can perform the same calculation when it receives a callback message. If the signature matches, it indicates the message is from Tencent Cloud.</td>
</tr></table>

>? A key is used for authentication. You can set it in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**. We recommend you set it to ensure data security.

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Callback message parameters

| Parameter | Type   | Description           |
| :----------- | :----- | :-------------------------- |
| app           | string | Push domain name         |
| appname       | string | Push path           |
| stream_param  | string | Push URL parameters                                        |
| stream_id    | string | Live stream name                  |
| channel_id   | string | Same as the stream name                |
| create_time | int64 | Unix timestamp when a screenshot is generated |
| file_size    | int    | Screenshot file size in bytes    |
| width        | int    | Screenshot width in pixels           |
| height       | int    | Screenshot height in pixels        |
| pic_url      | string | Screenshot file path (`/path/name.jpg`) |
| pic_full_url | string | Screenshot download URL                 |

### Sample callback message
<dx-codeblock>
::: json json
{
    "app":"test.app",
		
    "appname":"live",
    	
    "channel_id":"your_channelid",
    	
    "create_time":1622599925,
    	
    "event_type":200,
    	
    "file_size":30670,
    	
    "height":720,
    
    "pic_full_url":"http://your.cos.region.myqcloud.com/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "pic_url":"/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
    	
    "stream_id":"your_streamid",
    	
    "stream_param":"txSecret=ca3e25e5dc17a6f9909a9ae7281e300d&txTime=60B83800",
    	
    "t":1622600525,
    	
    "width":1280
}
:::
</dx-codeblock>










