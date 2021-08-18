## API Description

This API is used by the app backend to monitor users' one-to-one messages in real time, including:
- Records one-to-one messages sent in real time, for example, by recording a log or synchronizing the messages to other systems.
- Blocks users' requests to send one-to-one messages of any type, such as text, image, and custom messages.
- Modifies users' message content, for example, by filtering out restricted words or adding custom information defined by the app. Currently, this API cannot modify the content of rich media messages such as audio, image, file, and video, but can change these rich media messages to text or custom messages.

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding protocol for this callback. For more information on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and forbidding message sending is returned for the callback before sending one-to-one messages, the callback after sending one-to-one messages cannot be triggered.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and the message body is modified during the callback before sending one-to-one messages, the callback after sending one-to-one messages will use the modified message for callback.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a one-to-one message on the client.
- The app admin sends a one-to-one message by calling the `sendmsg` RESTful API.

## Callback Trigger Time

The IM backend has received a one-to-one message sent by a user but has not delivered the message to the target user.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**
```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS and the request method is POST. |
| [www.example.com](http://www.example.com) | Callback URL |
| SdkAppid | `SDKAppID` assigned by the IM console when an app is created |
| CallbackCommand | The value is always `C2C.CallbackBeforeSendMsg`. |
| contenttype | The value is always `JSON`. |
| ClientIP | IP address of the client, such as `127.0.0.1` |
| OptPlatform | Platform of the client. For more information about valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample requests

```
{
    "CallbackCommand": "C2C.CallbackBeforeSendMsg", // Callback command
    "From_Account": "jared", // Sender
    "To_Account": "Jonh", // Recipient
    "MsgSeq": 48374, // Sequence number of the message
    "MsgRandom": 2837546, // Random number of the message
    "MsgTime": 1557481126, // Timestamp in seconds indicating when the message is sent 
    "MsgKey": "48374_2837546_1557481126", // Unique identifier of the message. It can be used to recall the message via a RESTful API call.
    "OnlineOnlyFlag":1, // The value is `1` if it is an online message and `0` if it's not
    "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

### Request fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| From_Account | String | `UserID` of the message sender |
| To_Account | String | `UserID` of the message recipient |
| MsgSeq | Integer | Sequence number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgRandom | Integer | Random number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgTime | Integer | Timestamp in seconds indicating when the message is sent. <br>One-to-one messages are preferentially sorted by `MsgTime`. Messages sent in the same second are sorted by `MsgSeq`. Messages with larger values of `MsgSeq` are after those with smaller values. |
| MsgKey | String | Unique identifier of the message. It can be used to [recall the message](https://intl.cloud.tencent.com/document/product/1047/35015) via a RESTful API call. |
| OnlineOnlyFlag | Integer | The value is `1` if it is an online message and `0` if it's not. |
| MsgBody | Array | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData | String | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |

### Sample response when sending messages is allowed

The user is allowed to send messages, and the message content is not modified.

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // `0` indicates the user is allowed to send messages.
}
```

### Sample response when sending messages is forbidden

The user is not allowed to send group messages. In this case, the message is not sent, and the error code `20006` is returned to the user (message sender).

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // `1` indicates that the user is not allowed to send messages.
}
```

### Sample response when the message content is modified

In the following sample, the message sent by the user is modified (a custom message or custom message data is added), and the IM backend will send the modified message. With this feature, the app backend can add special content, such as the user level and title, to the message sent by the user.
**Example:**

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // This field must be set to `0` so that the modified message can be sent normally.
    "MsgBody": [ // Message modified by the app backend. If the app backend does not modify the message, the message sent by the user is delivered.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // Custom message
            "MsgContent": {
                "Desc": " CustomElement.MemberLevel ", // Description
                "Data": " LV1" // Data
            }
        }
    ],
    "CloudCustomData": "your new cloud custom data" // Custom message data
}
```

### Response fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Yes | Error code. `0`: allows sending messages. `1`: forbids sending messages. If the business side wants to forbid a user to send messages and send `ErrorCode` and `ErrorInfo` to the client, ensure that the value of `ErrorCode` is set within [120001, 130000]. |
| ErrorInfo | String | Yes | Error information |
| MsgBody | Array | No | Message body modified by the app backend. The IM backend sends the modified message to the recipient. For more information on the format, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData | String | No | Custom message data modified by the app backend. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. The IM backend sends the modified message to the recipient. |

References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback After Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34365)
- [Sending One-to-One Messages to One User](https://intl.cloud.tencent.com/document/product/1047/34919)
- [Sending One-to-One Messages to Multiple Users](https://intl.cloud.tencent.com/document/product/1047/34920)


