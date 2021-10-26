Live recording feature records live stream images in real time according to the recording template bound to the push domain name, and then stores the recording files in VOD. The recording callback is used to push the information of recording files, including the start time and end time of recording, as well as recording file ID, size and download URL. You need to configure the server address for receiving recording callback messages in the callback template, and bind the template to the push domain name. When a recording event is triggered by a live stream, the Tencent Cloud CSS backend will call back the recording file information to the configured receiving server.

This document describes the fields in callback message notifications sent by Tencent Cloud CSS after a recording callback event is triggered.

## Notes

- You need to understand how to configure callbacks and how you will receive messages via Tencent Cloud CSS before reading this document. For more information, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080).
- The recording video files are stored in the [VOD console](https://console.cloud.tencent.com/vod/overview) by default. You need to activate the VOD service first and ensure the VOD service has no overdue payments.
- When you call the [CreateRecordTask](https://intl.cloud.tencent.com/zh/document/product/267/37309) API, [stream_param](#message) parameters carried in the user push URL will not be returned in the recording callback. Yet if you use other recording methods, such parameters will be returned in the recording callback.
- After HLS recording resumption is enabled, no callback will be returned for push interruptions, and only callbacks for the final generated file will be returned.


## Recording Event Parameters
### Event type parameters

| Event Type | Parameter Value           |
| :------- | :------------- |
| Live recording | event_type = 100 |

<span id="public"></span> 
### Common callback parameters
<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. <li>The format of `t` is a decimal Unix timestamp, i.e., the number of seconds that have elapsed since 00:00:00 (UTC/GMT time), January 1, 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Event notification security signature sign = MD5(key + t). <br>Note: Tencent Cloud concatenates the encryption <a href="#key">key</a> and `t`, calculates the `sign` value through MD5, and places it in the notification message. When your backend server receives the notification message, it can confirm whether the `sign` is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.</td>
</tr></table>

>? <span id="key"></span>`key` is the callback key in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. We recommend filling in this field to ensure data security.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)


<span id="message"></span> 
### Callback message parameters

| Parameter | Type   | Description                                                         |
| :----------- | :----- | :--------------------------------------------------- |
| appid        | int    | User [APPID](https://console.cloud.tencent.com/developer)                                           |
| app           | string | Push domain name         |
| appname       | string | Push path           |
| stream_id     | string | Live stream name                 |
| channel_id    | string | Same as the live stream name                     |
| file_id      | string | VOD file ID, which uniquely identifies a VOD file on the [VOD platform](https://intl.cloud.tencent.com/document/product/266/33895) |
| file_format  | string | File format. Valid values: `flv`, `hls`, `mp4`, `aac`                               |
| task_id| string| ID of a recording task, which is valid only if the task is created using the [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309) API | 
| start_time   | int64  | Start timestamp of a recording file                                  |
| end_time     | int64  | End timestamp of a recording file                                |
| duration     | int64  | Duration of a recording file, in seconds                                 |
| file_size    | uint64 | Recording file size in pixels                               |
| stream_param  | string | User push URL parameters (custom)                                       |
| video_url    | string | Recording file download URL                                 |


<span id="example"></span> 
### Sample callback message

```
{
"event_type":100,

"appid":12345678,

"app":yourapp,

"appname":yourappname,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",
"task_id":"UpTbk5RSVhRQ********************0xTSlNTQltlRVRLU1JAWW9EUb",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e**********09a9ae7281e300d",

"t":1545030873
}
```




