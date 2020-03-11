## Feature Description

Through this callback, the app backend can monitor users’ one-to-one chat messages in real time, including:
- Recording one-to-one chat messages in real time (for example, recording the messages in a log or synchronizing them to other systems).
-  Intercepting users’ one-to-one chat requests.
-  Modifying users’ message content (for example, filtering sensitive words or adding app-defined custom information).

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the callback. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: The IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and the callback before sending one-to-one chat messages returns muting, then the callback after sending one-to-one chat messages will not be triggered.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and the callback before sending one-to-one chat messages modifies the message body, then the callback after sending one-to-one chat messages will use the modified message for callback.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

-  An app user uses a client to send a one-to-one chat message.
-  The app admin sends a one-to-one chat message through the RESTful API (sendmsg).

## Callback Triggering Time

The callback is triggered after the IM backend receives a one-to-one chat message sent by a user and before the IM backend sends the message to the target user.

## API Description

### Request URL example

In the following example, the callback URL configured by the app is `https://www.example.com`.
**Example:**
```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| [www.example.com](http://www.example.com) | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to C2C.CallbackBeforeSendMsg. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "C2C.CallbackBeforeSendMsg", // Callback command
    "From_Account": "jared", // Sender
    "To_Account": "Jonh", // Recipient
    "MsgSeq": 48374, // Message sequence number
    "MsgRandom": 2837546, // Message random number
    "MsgTime": 1557481126, // Message sending timestamp, in seconds 
    "MsgBody": [ // Message body. See the TIMMessage message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| From_Account | String | Identifier of the message sender |
| To_Account | String | Identifier of the message recipient |
| MsgSeq | Integer | Message sequence number for identifying this message |
| MsgRandom | Integer | Message random number for identifying this message |
| MsgTime | Integer | Message sending timestamp, in seconds |
| MsgBody | Array | Message body. For details, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Response packet example (with chat allowed)

Allows the user to chat without modifying the content of the message to be sent.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 0 indicates that chat is allowed.
}
```

### Response packet example (with muting enabled)

Mutes the user. Meanwhile, the message will not be sent, and the `20006` error code will be returned to the user (the message sender).

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // 1 indicates muting.
}
```

### Response packet example (with message content modified)

In the following response example, the one-to-one chat message sent by the user is modified (a custom message is added), and the IM backend will deliver the modified message. Based on this situation, the app backend can add some special content, such as the user level and title, to the message sent by the user.
**Example:**

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // The parameter value must be set to 0 so that the modified message can be normally delivered.
    "MsgBody": [ // The modified message by the app. If no modification is made, the message sent by the user is used by default.
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
    ]
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: allow chat. 1: mute. If the business requires that ErrorCode and ErrorInfo are sent to the client while muting is enabled, set ErrorCode to a value within the range of [120001, 130000]. |
| ErrorInfo | String | Required | Error information. |
| MsgBody | Array | Optional | The modified message body by the app. The IM backend will send the modified message to friends. For the detailed message format, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback after sending one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/34365)
- RESTful APIs: [Sending a one-to-one chat message](https://intl.cloud.tencent.com/document/product/1047/34919)
- RESTful APIs: [Sending one-to-one chat messages in batches](https://intl.cloud.tencent.com/document/product/1047/34920)
