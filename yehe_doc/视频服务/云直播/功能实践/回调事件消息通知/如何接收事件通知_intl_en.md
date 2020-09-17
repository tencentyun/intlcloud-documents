If an event configured in the template triggers the callback during live streaming, Tencent Cloud will send a request to your server which is responsible for the response. After authentication, a JSON packet of the callback can be obtained.

Currently, the following LVB events can trigger a notification: stream push, stream interruption, recording, screencapturing, and porn detection.

## Overall Process

<img src="https://main.qcloudimg.com/raw/ea1b7cd9ac91b2d561ef045c2f6f2159.svg" data-nonescope="true">

**Process description:**
1. The host configures event message notification URLs and related features such as recording and screencapturing in the console or by calling TencentCloud APIs.
2. The host pushes a stream or interrupts the push.
3. When an event occurs in the LVB service, a message will be sent to viewers through the event message notification service.
<span id="protocol"></span>
## Event Message Notification Protocol

### Network protocol
- Request: HTTP POST request with a JSON packet. The specific packet content of each type of message is described later.
- Response: HTTP STATUS CODE = 200. The server ignores the specific content of the response packet. For more accurate connection, we recommend you add JSON: `{"code":0}` to the response.

### Notification reliability

There is a retry mechanism for event notification service. Such retries will be made with an interval of 60 seconds for a total of 3 times. To avoid the impact of such retries on your server and network bandwidth, you should make sure that the response packet can be returned normally. A retry will be triggered in the following cases:

- No response packet is returned for a long time (at least 20 seconds).
- The HTTP status code in the response is not 200.

<span id="configuration"></span>
## Callback Event Configuration
Callback configuration can mainly be implemented in two ways: in the [LVB Console](#c_callback) and through [server API](#api_callback).
>?You can configure different callback URLs for LVB stream push, stream interruption, recording, screencapturing, and porn detection events.



<span id="c_callback"></span>
### LVB Console
1. Go to **Feature Template** > **[Callback Configuration](https://console.cloud.tencent.com/live/config/callback)** in the LVB Console to create a callback template. For detailed directions, please see [Creating Callback Template](https://intl.cloud.tencent.com/document/product/267/31074).
![](https://main.qcloudimg.com/raw/e487fbb21c3e7018c97f82f7055b8f8a.png)
2. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, find the target push domain name, and click **Manage** > **Template Configuration** to associate it with the callback template. For detailed directions, please see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31065).

### Server API<span id="api_callback"></span>
1. Call [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) to create a callback template and set the callback parameters you need.
2. Call [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) to create a callback rule, set the `DomainName` and `TemplateId` (returned in step 1) parameters, and enter the same `AppName` as in the push and playback addresses to enable callback for certain live streams.

## Callback Message Parameter Description
After the callback template is successfully associated with the domain name, when a template event is triggered during live streaming, Tencent Cloud will actively send a JSON packet containing the callback message to your server. Specific parameters of the callback message are described as follows:
- [Stream push event message notification](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [Stream interruption event message notification](https://intl.cloud.tencent.com/zh/document/product/267/38081)
- [Recording event message notification](https://intl.cloud.tencent.com/zh/document/product/267/38082)
- [Screencapturing event message notification](https://intl.cloud.tencent.com/zh/document/product/267/38083)
- [Porn detection event message notification](https://intl.cloud.tencent.com/zh/document/product/267/38084)






