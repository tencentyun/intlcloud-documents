The live screencapture feature is used to take screenshots of a real-time live stream at regular intervals and generate images. You can get the information of screenshots from callback notifications. Such screenshot data can be used for porn detection, live room cover generation, and other scenarios.

## Notes

- You need to understand how to configure the callback feature and receive callback messages on Tencent Cloud CSS before reading this document. For more information, please see [How to Receive Event Notification](https://intl.cloud.tencent.com/zh/document/product/267/38080).
- The screenshot information obtained after a screencapturing callback event is triggered can be used for porn detection, live room cover generation, and other scenarios.

## Screencapturing Event Parameter Description

### Event type parameters

| Event Type | Field Value Description           |
| :------- | :------------- |
| Live screencapture | event_type = 200 |

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

>? `key` is the callback key in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. In order to protect the security of your data, we recommend you enter it.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Callback message parameters


| Field Name | Type   | Description                                                         |
| :----------- | :----- | :-------------------------- |
| stream_id    | string | Live stream name                  |
| channel_id   | string | The value is the same as live stream name                |
| create_time | int64 | Unix timestamp when a screenshot is generated |
| file_size    | int    | Screenshot file size in bytes    |
| width        | int    | Screenshot width in pixels           |
| height       | int    | Screenshot height in pixels          |
| pic_url      | string | Screenshot file path, such as `/path/name.jpg` |
| pic_full_url | string | Screenshot download URL                 |

### Sample callback message

```
{
"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```








