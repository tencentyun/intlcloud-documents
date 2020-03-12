## Feature Description

The app backend can use this callback to monitor users’ group messages in real time. Through this callback, the app backend can be notified of the successfully sent group messages so that it can perform required data synchronization.

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

-  An app user sends a group message through the client.
-  The app admin sends a group message through a RESTful API.

## Callback Triggering Time

The callback is triggered after a group message is successfully sent.

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
| CallbackCommand | The value is fixed to Group.CallbackAfterSendMsg. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
    "MsgSeq": 123, // Message sequence number
    "MsgTime": 1490686222, // Message sending time
    "MsgBody": [ // Message body. For more information, see the TIMMessage message object.
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
| GroupId | String | The ID of the group that generates group messages. |
| Type | String | The type of the group that generates group messages, such as Private, Public, or ChatRoom. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E7.BB.84.E5.BD.A2.E6.80.81.E4.BB.8B.E7.BB.8D). |
| From_Account | String | The identifier of the message sender. |
| Operator_Account | String | The identifier of the message initiator, based on which the system can identify whether the request is initiated by the admin. |
| Random | Integer | A 32-bit random number in the message sending request. |
| MsgSeq | Integer | The message sequence number, which is the unique identifier of a message. |
| MsgTime | Integer | The message sending timestamp corresponding to the backend server time. |
| MsgBody | Array | The message body. For details, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Response packet example

After data synchronization, the app backend sends a callback response packet.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The result in the response is ignored.
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: ignore the result in the response. |
| ErrorInfo | String | Required | Error information. |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Sending common messages in a group](https://intl.cloud.tencent.com/document/product/1047/34959)
