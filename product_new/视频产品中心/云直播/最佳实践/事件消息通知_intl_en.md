

When an LVB event is triggered, you can use the event message notification to receive the event information. Message notifications are supported for the following events:

- **LVB push** event
- **LVB push interruption** event
- **LVB screencapturing** file generation event

>This document does not cover the callback notification for porn detection events. For more information, see [Best Practices - LVB Porn Detection](https://intl.cloud.tencent.com/document/product/267/31564).

## Event Message Notification Flow

![](https://main.qcloudimg.com/raw/009a55d2fc7e56d17a3cb221b9765647.png)

Overall process:
1. The host configures an event message notification URL and related features such as screencapturing in the console or through TencentCloud APIs.
- The host pushes a stream or interrupts the push.
- When an event occurs inside the LVB service, a message will be sent to viewers via the event message notification service.

## Event Message Notification Configuration

The event message notification can be configured with the:
- TencentCloud API
- Console

Different event message notification URLs can be configured for different types of events, including:
- Push event notification URL (StreamBeginNotifyUrl)
- Push interruption event notification URL (StreamEndNotifyUrl)
- Screencapturing event notification URL (SnapshotNotifyUrl)

## Event Message Notification Protocol

**Network protocol**

Request: HTTP POST request with a JSON packet. The specific packet content of each type of message is described later.

Response: HTTP STATUS CODE = 200. The server ignores the specific content of the response packet. For protocol-friendliness, it is recommended to add JSON: `{"code":0}` to the response.

**Notification reliability**

The event notification service has a retry mechanism with an interval of 60 seconds for a total of 3 retries. In order to avoid the impact of retries on your server and network bandwidth, make sure that the response packet can be returned normally. A retry is triggered in the following cases:
- No response packet is returned for a long time (at least 20 seconds).
- The HTTP status code in the response is not 200.

## Event Message Notification Parameter Descriptions

### Common Parameter Description

| Field Name | Type | Description |
| --- | --- | --- |
| event\_type | int | Event notification message type. 1: push event; 0: push interruption event; 200: screencapturing event |
| sign | string | Event notification signature |
| t | int64 | Event notification signature expiration time (UNIX timestamp) |

- t (expiration time): The default expiration time of a message notification from Tencent Cloud is 10 minutes. If the time specified by the t value in a message notification has elapsed, it can be determined that this notification is invalid, thereby preventing network replay attacks. The format of t is a decimal UNIX timestamp, i.e., the number of seconds that has elapsed since January 1, 1970 00:00 (UTC/GMT time).
- sign (security signature): sign = MD5(key + t). Tencent Cloud splices the encryption key and t, calculates the sign value through MD5, and places it in the notification message. After your backend server receives the notification message, it can confirm whether the sign is correct based on the same algorithm and then determine whether the message is indeed from the Tencent Cloud backend.
>key is the callback key configured in the callback as shown below:
>![](https://main.qcloudimg.com/raw/6d170460342946de0f21cce5f9985408.png)

### Message Bodies in Various Types

**LVB push and push interruption events**

- For an LVB push event, event\_type = 1
- For an LVB push interruption event, event\_type = 0

| Field Name | Type | Description |
| --- | --- | --- |
| appid | int | User APPID |
| app | string | Push domain name |
| appname | string | Push path |
| stream\_id | string | Stream name |
| channel\_id | string | Same as the stream name |
| event\_time | int64 | UNIX timestamp when the event message is generated |
| sequence | string | Message serial number that identifies a push activity. The same push activity generates push and interruption messages with the same serial number |
| node | string | IP of the LVB access point |
| user\_ip | string | User's push IP |
| stream\_param | string | Parameters in the user's push URL |
| push\_duration | string | Push duration in the push interruption event notification in milliseconds |
| errcode | int | Push interruption error code |
| errmsg | string | Push interruption error message |

- errcode (push interruption error code)

| Error Code | Error Description | Reason |
| --- | --- | --- |
| 1 | recv rtmp deleteStream | The host actively interrupted the push |
| 2 | recv rtmp closeStream | The host actively interrupted the push |
| 3 | recv() return 0 | The host actively closed the TCP connection |
| 4 | recv() return error | Exception with the TCP connection to the host |
| 7 | rtmp message large than 1M | Exception with the received stream data |
| Other | LVB service internal exception | If you need help, contact your Tencent Cloud sales rep or submit a ticket |

Sample:

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

"stream_id":" test_stream",

"stream_param":"stream_param=test",

"user_ip":"119.29.94.245",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873

}
```

**LVB screencapturing file generation event**

- event\_type = 200

| Field Name | Type | Description |
| --- | --- | --- |
| stream\_id | string | Stream name |
| channel\_id | string | Same as the stream name |
| create\_time | int64 | UNIX timestamp when the screenshot is generated |
| file\_size | int | Screenshot file size in bytes |
| width | int | Screenshot width in pixels |
| height | int | Screenshot height in pixels |
| pic\_url | string | Screenshot file path /path/name.jpg |
| pic\_full\_url | string | Screenshot download URL |

Sample:

```
{

"event_type":200,

"stream_id":"stream_name",

"channel_id":" stream_name",

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
