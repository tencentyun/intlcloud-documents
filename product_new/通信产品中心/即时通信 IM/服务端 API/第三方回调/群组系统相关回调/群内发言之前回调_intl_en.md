## Feature Description

The app backend can use this callback to monitor users’ group messages in real time, including:
- Recording group messages in real time, for example, recording a log or synchronizing the messages to other systems
- Blocking users’ requests for sending group messages
-  Modifying the content of users’ messages, for example, filtering out sensitive words or adding custom information defined by the app

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user sends a group message through the client.
- The app admin sends a group message through a RESTful API.

## Callback Triggering Time

The callback is triggered before the IM backend sends a group message to group members.

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
| CallbackCommand | The value is fixed to Group.CallbackBeforeSendMsg. |
| contenttype | The value is fixed to JSON. |
| ClientIP | The client IP address, whose format is similar to 127.0.0.1. |
| OptPlatform | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
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
| MsgBody | Array | The message body. For details, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Response packet example

#### Allowing to send a group message

The user is allowed to send a group message, and the content of the sent message is not modified.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The 0 value indicates allowing to send group messages.
}
```

#### Disallowing to send a group message

The user is not allowed to send a group message. In this case, the message is not sent, and the error code `10016` is returned to the caller.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // The 1 value indicates that the user is disallowed to send group messages.
}
```

#### Discarding a message silently

The user is not allowed to send a group message. In this case, the message is not sent, but a successful sending message will be returned to the caller to pretend that the message has been sent.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 2 // The 2 value indicates the message is silently discarded.
}
```

#### Modifying message content

In the following response example, the group message sent by the user is modified (in this case, a custom message is added), and the IM backend will deliver the modified message. With this feature, the app backend can add special content, such as the user level and title, to the message sent by the user.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // The parameter value must be 0 so that the modified message can be sent normally.
    "MsgBody": [ // The message modified by the app. If no modification is made, the message sent by the user is used by default.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // Custom message
            "MsgContent": {
                "Desc": "CustomElement.MemberLevel", // Description
                "Data": "LV1" // Data
            }
        }
    ]
}
```

### Response packet fields

| Field | Type | Attribute | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code. 0: allow to send group message. 1: disallow to send group messages. 2: the sent message will be silently discarded. |
| ErrorInfo | String | Required | Error information. |
| MsgBody | Array | Optional | The message body modified by the app. The IM backend will send the modified message to the group. For details on the format, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Sending common messages in a group](https://intl.cloud.tencent.com/document/product/1047/34959)
