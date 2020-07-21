After a push domain name is [associated with a callback template](https://intl.cloud.tencent.com/document/product/267/31065), if an event configured in the template triggers the callback during a live streaming, Tencent Cloud will actively send a request to the customer server which is responsible for the response. After verification, a JSON packet of the callback can be obtained.
Currently, the following events in a live streaming can trigger a notification:

- [**LVB push** event](#DropLiveStream)
- [**LVB stream interruption** event](#DropLiveStream)
- [**LVB recording** file generation event](#Record)
- [**LVB screenshot** file generation event](#Screenshot)

>! This document does not cover the callback notification for porn detection events. For more information, see [Best Practice - LVB Porn Detection](https://intl.cloud.tencent.com/document/product/267/31564).


## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live) and added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970). 
- You have created a [callback template](https://intl.cloud.tencent.com/document/product/267/31074) and [associated it with a push domain name](https://intl.cloud.tencent.com/document/product/267/31065).

## Event Message Notification Flow
![](https://main.qcloudimg.com/raw/5703b324ae1b05cfc97efa59f30e2c6c.jpg)

Overall process:
1. The host configures an event message notification URL and related features such as recording and screencapturing in the console or through TencentCloud APIs.
2. The host pushes or interrupts a stream.
3. When an event occurs in the LVB service, a message will be sent to viewers via the event message notification service.

## Event Message Notification Configuration

The event message notification can be configured with:
- [LVB APIs v3.0](https://intl.cloud.tencent.com/document/product/267/30760)
- [LVB Console](https://intl.cloud.tencent.com/document/product/267/31566)

Different event message notification URLs can be configured for different types of events, including:
- Push event notification URL (StreamBeginNotifyUrl)
- Stream interruption event notification URL (StreamEndNotifyUrl)
- Recording event notification URL (RecordNotifyUrl)
- Screencapturing event notification URL (SnapshotNotifyUrl)

## Event Message Notification Protocol

### Network protocol
- Request: HTTP POST request with a JSON packet. The specific packet content of each type of message is described later.
- Response: HTTP STATUS CODE = 200. The server ignores the specific content of the response packet. For more accurate connection, it is recommended to add `JSON: `{"code":0}`` to the response.

### Notification reliability
The event notification service has a retry mechanism with an interval of 60 seconds for a total of 3 retries. In order to avoid the impact of retries on your server and network bandwidth, make sure that the response packet can be returned normally. A retry is triggered in the following cases:
- No response packet is returned for a long time (at least 20 seconds).
- The HTTP status code in the response is not 200.

## Event Message Notification Parameter Descriptions

### Common parameter description

| Field Name | Type | Description |
| --- | --- | --- |
| event\_type | int | Event notification message type. 1: push event; 0: stream interruption event; 100: recording event; 200: screencapturing event |
| sign | string | Event notification signature |
| t | int64 | Event notification signature expiration time (UNIX timestamp) |

- **t (expiration time)**: the default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the `t` value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. The format of `t` is a decimal UNIX timestamp, i.e., the number of seconds that have elapsed since January 1, 1970 00:00 (UTC/GMT time).
- **sign (security signature)**: sign = MD5(key + t). Tencent Cloud splices the encryption `key` and `t`, calculates the `sign` value through MD5, and places it in the notification message. After your backend server receives the notification message, it can confirm whether the `sign` is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.
>?`key` is the callback key in **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)**, which is mainly used for authentication. In order to protect the security of your data, we recommend that you enter it.

![](https://main.qcloudimg.com/raw/15f7e94dcabfb52de5e0bb93c1380be2.png)


### Message bodies in various types
<span id="DropLiveStream"></span>
#### LVB push and stream interruption events
- For an LVB push event, `event\_type` = 1
- For an LVB stream interruption event, `event\_type` = 0
<table>
<thead><tr><th>Field Name</th><th>Type</th><th>Description</th></tr></thead>
<tbody><tr>
<td>appid</td>
<td>int</td>
<td>User `APPID`</td>
</tr><tr><td>app</td>
<td>string</td>
<td>Push domain name</td>
</tr><tr><td>appname</td>
<td>string</td>
<td>Push path</td>
</tr><tr><td>stream_id</td>
<td>string</td>
<td>Live stream name</td>
</tr><tr><td>channel_id</td>
<td>string</td>
<td>Same as the live stream name</td>
</tr><tr><td>event_time</td>
<td>int64</td>
<td>UNIX timestamp when the event message is generated</td>
</tr><tr><td>sequence</td>
<td>string</td>
<td>Sequence number of the message, which indicates a push event. A push event generates push and stream interruption messages with the same sequence number.</td>
</tr><tr><td>node</td>
<td>string</td>
<td>IP of the LVB access point</td>
</tr><tr><td>user_ip</td>
<td>string</td>
<td>User's push IP</td>
</tr><tr><td>stream_param</td>
<td>string</td>
<td>Parameters in the user's push URL</td>
</tr><tr><td>push_duration</td>
<td>string</td>
<td>Push duration in the stream interruption event notification in milliseconds</td>
</tr><tr><td>errcode</td>
<td>int</td>
<td>Stream interruption error codes</td>
</tr><tr><td>errmsg</td>
<td>string</td>
<td>Description of stream interruption errors</td>
</tr>
</tbody></table>
- errcode (stream interruption error codes)
<table>
<thead><tr><th>Error Code</th><th>Description</th><th>Reason</th></tr></thead>
<tbody><tr>
<td>1</td>
<td>recv rtmp deleteStream</td>
<td>The host actively interrupted the stream</td>
</tr><tr><td>2</td>
<td>recv rtmp closeStream</td>
<td>The host actively interrupted the stream</td>
</tr><tr><td>3</td>
<td>recv() return 0</td>
<td>The host actively closed the TCP connection</td>
</tr><tr><td>4</td>
<td>recv() return error</td>
<td>Exception with the TCP connection to the host </td>
</tr><tr><td>7</td>
<td>rtmp message large than 1M</td>
<td>Exception with the received stream data</td>
</tr><tr><td>Others</td>
<td>LVB service internal exception</td>
<td>If you need help, contact your Tencent Cloud sales rep or submit a ticket</td>
</tr>
</tbody></table>

**Sample:**

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

<span id="Record"></span>
#### **LVB recording** file generation event

- event\_type = 100
<table>
<thead><tr><th>Field Name</th><th>Type</th><th>Description</th></tr></thead>
<tbody><tr>
<td>appid</td>
<td>int</td>
<td>User `APPID`</td>
</tr><tr><td>stream_id</td>
<td>string</td>
<td>Live stream name</td>
</tr><tr><td>channel_id</td>
<td>string</td>
<td>Same as the live stream name</td>
</tr><tr><td>file_id</td>
<td>string</td>
<td>VOD file ID, which uniquely identifies a VOD file in the VOD system</td>
</tr><tr><td>file_format</td>
<td>string</td>
<td>flv, hls, mp4, aac</td>
</tr><tr><td>start_time</td>
<td>int64</td>
<td>Start timestamp of the recording file</td>
</tr><tr><td>end_time</td>
<td>int64</td>
<td>End timestamp of the recording file</td>
</tr><tr><td>duration</td>
<td>int64</td>
<td>Recording file duration in seconds</td>
</tr><tr><td>file_size</td>
<td>uint64</td>
<td>Recording file size in bytes</td>
</tr><tr><td>stream_param</td>
<td>string</td>
<td>Parameters in the user's push URL</td>
</tr><tr><td>video_url</td>
<td>string</td>
<td>Recording file download URL</td>
</tr>
</tbody></table>

**Sample:**
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

<span id="Screenshot"></span>
#### **LVB screenshot** file generation event

- event\_type = 200
<table>
<thead><tr><th>Field Name</th><th>Type</th><th>Description</th></tr></thead>
<tbody><tr>
<td>stream_id</td>
<td>string</td>
<td>Live stream name</td>
</tr><tr><td>channel_id</td>
<td>string</td>
<td>Same as the live stream name</td>
</tr><tr><td>create_time</td>
<td>int64</td>
<td>UNIX timestamp when the screenshot is generated</td>
</tr><tr><td>file_size</td>
<td>int</td>
<td>Screenshot file size in bytes</td>
</tr><tr><td>width</td>
<td>int</td>
<td>Screenshot width in pixels</td>
</tr><tr><td>height</td>
<td>int</td>
<td>Screenshot height in pixels</td>
</tr><tr><td>pic_url</td>
<td>string</td>
<td>Screenshot file path: /path/name.jpg.</td>
</tr><tr><td>pic_full_url</td>
<td>string</td>
<td>Screenshot download URL</td>
</tr>
</tbody></table>

**Sample:**
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
