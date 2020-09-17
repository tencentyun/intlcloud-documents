After LVB recording is enabled, you can configure the registered callback domain name in the LVB recording callback template to have the LVB backend call back the recording result.

# Notes

- You need to understand how to configure the callback feature and receive callback messages on Tencent Cloud LVB before reading this document. For more information, please see [How to Receive Event Notification](https://intl.cloud.tencent.com/zh/document/product/267/38080).
- The recorded video files are stored in the [VOD Console](https://console.cloud.tencent.com/vod/overview) by default. We recommend you activate the VOD service in advance and purchase appropriate resource packages so as to avoid service suspension due to account arrears.


## Recording Event Parameter Description

### Event type parameters

| Event Type | Field Value Description           |
| :------- | :------------- |
| LVB recording | event_type = 100 |

### Common callback parameters
<table>
<tr><th>Field Name</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. <li>The format of `t` is a decimal Unix timestamp, i.e., the number of seconds that has elapsed since January 01, 1970 00:00 (UTC/GMT time).</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Security signature of event notification (sign = MD5(key + t)). <br>Note: Tencent Cloud splices the encryption `<a href="#key">key</a>` and `t`, calculates the `sign` value through MD5, and places it in the notification message. After your backend server receives the notification message, it can confirm whether the `sign` is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.</td>
</tr></table>

>? `<span id="key"></span>key` is the callback key in **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. In order to protect the security of your data, we recommend you enter it.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)


### Callback message parameters

| Field Name | Type | Description |
| :----------- | :----- | :--------------------------------------------------- |
| appid        | int    | User [APPID](https://console.cloud.tencent.com/developer)                                           |
| stream_id    | string | LVB stream name                                           |
| channel_id   | string | The value is the same as LVB stream name                                         |
| file_id      | string | VOD file ID, which can uniquely locate a VOD video file on the [VOD platform](https://intl.cloud.tencent.com/zh/document/product/266/33895) || file_format  | string | flv, hls, mp4, aac                                   |
| start_time   | int64  | Start timestamp of recording file                                   |
| end_time     | int64  | End timestamp of recording file                                 |
| duration     | int64  | Duration of recording file in seconds                                 |
| file_size    | uint64 | Recording file size in bytes                               |
| stream_param | string | User push URL parameters                                |
| video_url    | string | Recording file download URL                                 |

### Sample callback message

```
{
"event_type":100,

"appid":12345678,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```





