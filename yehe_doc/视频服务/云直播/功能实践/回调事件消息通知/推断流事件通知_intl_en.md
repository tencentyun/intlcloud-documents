Stream push/interruption callback is used to call back the push status information, including whether the push is successful or interrupted. You need to configure the server address for receiving push/interruption callback messages in a callback template and bind the template with the push domain name. When push starts via the generated push URL, Tencent Cloud backend will call back the push results to the server you set.

This document describes the parameters in callback message notifications sent by Tencent Cloud CSS after a stream push/interruption callback event is triggered.

## Note
You need to understand how to configure callbacks and how to receive messages on Tencent Cloud CSS before reading this document. For more information, see [How to Receive Event Notification](https://intl.cloud.tencent.com/document/product/267/38080). 


## Stream Push/Interruption Event Parameters
### Event type parameters

| Event Type | Parameter Value |
|---------|---------|
| Live push | event_type = 1 |
| Live stream interruption | event_type = 0 |

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

>? [](id:key)`key` is the callback key in **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. We recommend filling in this field to ensure data security.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### Callback message parameters

| Parameter | Type   | Description           |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | User [APPID](https://console.cloud.tencent.com/developer)      |
| app           | string | Push domain name         |
| appname       | string | Push path           |
| stream_id     | string | Live stream name                 |
| channel_id    | string | Same as the live stream name                     |
| event_time    | int64  | UNIX timestamp when the event message is generated               |
| sequence      | string | Message serial number, which is used to identify a push event. A push event generates push and interruption messages with the same serial number. |
| node          | string |  Upstream node IP                                          |
| user_ip       | string | User push IP                                                  |
| stream_param  | string | User push URL parameters                                        |
| push_duration | string | Push duration of the interrupted stream in milliseconds                               |
| errcode       | int    | Stream push/interruption error code                      |
| errmsg        | string | Stream push/interruption error message                                               |
| set_id          | int  | Whether the push is from inside the Chinese mainland. 1-6: yes; 7-200: no  |
|width       |  int   |Video width. This value may be `0` if the video header information is missing in the callback of the beginning of live push.  |
|height       |  int   |Video height. This value may be `0` if the video header information is missing in the callback of the beginning of live push.  |

### Stream push and interruption error codes
For error codes and error messages of stream push/interruption, see [Stream interruption error codes](https://intl.cloud.tencent.com/document/product/267/31083).

### Sample callback message
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
