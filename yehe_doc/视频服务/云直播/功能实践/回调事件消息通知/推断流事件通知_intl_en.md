After an LVB feature is enabled, you can configure the registered callback domain name in the push callback template to have the LVB backend call back the push result.
You need to understand how to receive messages on Tencent Cloud LVB before reading this document. For more information, please see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080). 


## Stream Push/Interruption Event Parameter Description

### Event type parameters

| Event Type | Field Value Description |
|---------|---------|
| LVB push | event_type = 1 |
| LVB stream interruption | event_type = 0 |

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
>![](https://main.qcloudimg.com/raw/34b21b2d50d2aca00dd2dfa19816e8e3.png)

### Callback message parameters

| Field name | Type   | Description                                                         |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | User [APPID](https://console.cloud.tencent.com/developer)                                                   |
| app           | string | Push domain name                                                     |
| appname       | string | Push path                                                     |
| stream_id     | string | LVB stream name                                                   |
| channel_id    | string | The value is the same as LVB stream name                                                 |
| event_time    | int64  | Unix timestamp of event message generation                                   |
| sequence      | string | Message serial number, which is used to identify a push event. A push event generates push and interruption messages with the same serial number |
| node          | string | LVB access point IP                                              |
| user_ip       | string | User push IP                                                  |
| stream_param  | string | User push URL parameters                                        |
| push_duration | string | Push duration of stream interruption event notification in milliseconds                               |
| errcode       | int    | Error code of stream interruption                                                 |
| errmsg        | string | Error description of stream interruption                                               |

### Stream push/interruption error codes

| errcode | Error Description                    | Cause                               |
| :----- | :------------------------- | :------------------------------------- |
| 1      | recv rtmp deleteStream     | The host interrupts the stream                         |
| 2      | recv rtmp closeStream      | The host interrupts the stream                         |
| 3      | recv() return 0            | The host disconnects the TCP connection                         |
| 4      | recv() return error        | A TCP connection exception occurs for the host                    |
| 7      | rtmp message large than 1M | An exception occurs in the received streaming data                         |
| Others   | LVB service internal exception           | If you need help, contact your Tencent Cloud sales rep or submit a ticket |

### Sample callback message
```
{
"app":"test.domain.com",

"appid":12345678,

"appname":"live",

"channel_id":"test_stream",

"errcode":0,

"errmsg":"ok",

"event_time":1545115790,

"event_type":1,

"node":"100.121.160.92",

"sequence":"6674468118806626493",

"stream_id":"test_stream",

"stream_param":"stream_param=test",

"user_ip":"119.29.94.245",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```
