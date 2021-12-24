If an event configured in the template triggers a callback during live streaming, Tencent Cloud will send a request to the customer’s server which is responsible for the response. After passing the verification, the server will obtain a JSON packet of the callback.

Currently, the following events can trigger a notification during live streaming: stream push, stream interruption, recording, screencapture and porn detection.

## Overall Process

<img src="https://main.qcloudimg.com/raw/252b7e06b322350c8520283e7826d5a3.png" data-nonescope="true">

**Process Description:**
1. The host configures event message notification URLs and features such as recording and screencapture in the console or by calling TencentCloud APIs.
2. The host pushes and stops the stream.
3. When an event occurs, a message will be sent to the customer backend via the event message notification service.


[](id:protocol)
## Event Message Notification Protocol

### Network protocol
- Request: HTTP POST request with a JSON packet. The specific packet content of each type of message is described later.
- Response: HTTP status code = 200. The server ignores the specific content of the response packet. For protocol-friendliness, we recommend you add `JSON: `{"code":0}`` to the response.

### Notification reliability
The event notification service has a retry mechanism. For the screencapture event, up to 5 retries will be made at an interval of 2 minutes. For the stream push, stream interruption, recording, and porn detection events, up to 12 retries will be made at an interval of 1 minute.
To prevent frequent retries from placing too much strain on your server and bandwidth, make sure response packets are returned as expected. A retry is triggered in the following cases:
- No response packet is returned for a long time (at least 20 seconds).
- The HTTP status code in the response is not `200`.

[](id:configuration)
## How to Configure Event Callbacks
You can configure callbacks via the [CSS console](#c_callback) or [server APIs](#api_callback).
>?CSS allows you to configure callback URLs separately for events of stream push, stream interruption, recording, screencapture and porn detection.



[](id:c_callback)
### CSS console
1. Log in to the CSS console and click **Event Center** > **[Live Stream Callback](https://console.cloud.tencent.com/live/config/callback)** to create a callback template. For detailed directions, see [Creating a Callback Template](https://intl.cloud.tencent.com/document/product/267/31074).
2. Click **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, find the target push domain name, and click **Manage** > **Template Configuration** to bind it with the callback template. For detailed directions, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/267/31065).

[](id:api_callback)
### Server APIs
1. Call the [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815) API to create a callback template and set the callback parameters.
2. Call the [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) API to set the `DomainName` (push domain name) and `TemplateId` (returned in step 1) parameters. Enter the `AppName` in the push and playback URLs to enable callback for specific live streams.

## Callback Parameters
After the template is successfully bound with the domain name, if an event configured in the template is triggered during the live streaming, Tencent Cloud will send a JSON packet containing the callback information to the customer’s server. The callback parameters are detailed as below:
- [Stream push event notification](https://intl.cloud.tencent.com/document/product/267/38081)
- [Stream interruption event notification](https://intl.cloud.tencent.com/document/product/267/38081)
- [Recording event notification](https://intl.cloud.tencent.com/document/product/267/38082)
- [Screencapture event notification](https://intl.cloud.tencent.com/document/product/267/38083)
- [Porn detection event notification](https://intl.cloud.tencent.com/document/product/267/38084)






