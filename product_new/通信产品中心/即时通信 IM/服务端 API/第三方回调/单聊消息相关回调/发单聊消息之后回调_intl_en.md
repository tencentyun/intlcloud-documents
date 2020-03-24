## Feature Description

Through this callback, the app backend can monitor users’ one-to-one chat messages in real time, including:
- Recording one-to-one chat messages in real time (for example, recording a log or synchronizing messages to other systems).
- Calculating statistics for one-to-one chat messages (for example, the number of users or that of messages).

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and the callback before sending one-to-one chat messages returns muting, the callback after sending one-to-one chat messages will not be triggered.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and the callback before sending one-to-one chat messages modifies the message body, the callback after sending one-to-one chat messages will use the modified message for callback.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

-  An app user uses a client to send a one-to-one chat message.
-  The app admin sends a one-to-one chat message through the RESTful API (SendMsg).

## Callback Triggering Time

The callback is triggered after the IM backend receives a one-to-one chat message sent by a user and sends the message to the target user.

> If the message fails to be delivered (for example, due to illegal word filtering), this callback will still be triggered.

## API Description

### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned by the IM console when an app is created. |
| CallbackCommand | The value is fixed to C2C.CallbackAfterSendMsg. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "C2C.CallbackAfterSendMsg", // Callback command
    "From_Account": "jared", // Sender
    "To_Account": "Jonh", // Recipient
    "MsgSeq": 48374, // Message sequence number
    "MsgRandom": 2837546, // Message random number
    "MsgTime": 1557481126, // Message sending timestamp, in seconds 
    "MsgBody": [ // Message body
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
| CallbackCommand | String | The callback command. |
| From_Account | String | The UserID  of the message sender. |
| To_Account | String | The UserID  of the message recipient. |
| MsgSeq | Integer | The message sequence number for identifying this message. |
| MsgRandom | Integer | The message random number for identifying this message. |
| MsgTime | Integer | The message sending timestamp in seconds. |
| MsgBody | Array | The message body. For details, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Response packet example

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // 0: the callback succeeded. 1: an error occurred during the callback.
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: the callback succeeded. 1: an error occurred during the callback. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback before sending one-to-one chat messages](https://intl.cloud.tencent.com/document/product/1047/34364)
- RESTful APIs: [Sending a one-to-one chat message](https://intl.cloud.tencent.com/document/product/1047/34919)
- RESTful APIs: [Sending one-to-one chat messages in batches](https://intl.cloud.tencent.com/document/product/1047/34920)
