The stream pushing callback informs you whether stream pushing is successful or interrupted. You need to configure a server address for the callback in a callback template and bind the template with your push domain name. After push starts via a URL generated under the domain, the Tencent Cloud backend will send the callback to the server you set.

This document describes the parameters in a stream pushing callback notification sent to you by CSS.

## Note
This guide assumes that you understand how to configure callbacks and receive callback notifications from CSS. For details, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080). 


## Stream Pushing Event Parameters
### Event type

| Event Type | Value           |
|---------|---------|
| Successful push | event_type = 1 |
| Push interrupted | event_type = 0 |

### Common callback parameters
<table>
<tr><th>Parameter</th><th>Type</th><th>Description</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>Expiration time, which is the Unix timestamp when the event notification signature expires. <ul style="margin:0"><li>The default validity period of a callback notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a notification has elapsed, then this notification is considered invalid. This prevents network replay attacks. <li>The value of `t` is a decimal Unix timestamp, that is, the number of seconds that have elapsed since 00:00:00 (UTC/GMT time), January 1, 1970.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>Security signature. sign = MD5(key + t). <br>Tencent Cloud splices the encryption <a href="#key">key</a> and `t`, generates the MD5 hash of the spliced string, and embeds it in callback messages. Your backend server can perform the same calculation when it receives a callback message. If the signature matches, it indicates the message is from Tencent Cloud.</td>
</tr></table>

>? [](id:key)You can set the callback key in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, which is used for authentication. We recommend you set this field to ensure data security.
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Callback parameters

| Parameter | Type   | Description           |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | User [APPID](https://console.cloud.tencent.com/developer)      |
| app           | string | Push domain name         |
| appname       | string | Push path           |
| stream_id     | string | Live stream name                 |
| channel_id    | string | Same as the live stream name                     |
| event_time    | int64  | UNIX timestamp when the event message is generated               |
| sequence      | string | Message sequence number, which identifies a push. The notifications for a push, whether they are for successful push or stream interruption, have the same sequence number. |
| node          | string |  IP of the live stream access point                                              |
| user_ip       | string | User push IP                                                  |
| stream_param  | string | User push URL parameters                                        |
| push_duration | string | Push duration of the interrupted stream in milliseconds                               |
| errcode       | int    | Stream pushing error code                      |
| errmsg        | string | Stream pushing error message                                               |
| set_id          | int  | Whether the push is from inside the Chinese mainland. 1-6: yes; 7-200: no.  |
|width       |  int   |Video width. The value of this parameter may be `0` if the video header information is missing at the beginning of a push.  |
|height       |  int   |Video height. The value of this parameter may be `0` if the video header information is missing at the beginning of a push.  |

### Causes of stream interruption
For a list of the causes of stream interruption, see [Stream Interruption Records](https://intl.cloud.tencent.com/document/product/267/31083).

### Sample callback
```JSON
{
	"app":"test.domain.com",
	
	"appid":12345678,
	
	"appname":"live",
	
	"channel_id":"test_stream",
	
	"errcode":0,
	
	"errmsg":"ok",
	
	"event_time":1545115790,
	
	"event_type":1,
	
	"set_id":2,
	
	"node":"100.121.160.92",
	
	"sequence":"6674468118806626493",
	
	"stream_id":"test_stream",
	
	"stream_param":"stream_param=test",
	
	"user_ip":"119.29.94.245",
	
	"width": 0,
	
	"height": 0,
	
	"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
	
	"t":1545030873
}
```
