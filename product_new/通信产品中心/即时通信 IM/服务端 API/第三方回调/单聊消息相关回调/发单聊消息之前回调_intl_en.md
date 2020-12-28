## Feature Description

This API is used by the app backend to monitor a user’s one-to-one chat messages in real time, including:
- Records one-to-one chat messages in real time, for example, by recording a log or synchronizing the messages to other systems.
- Intercepts a user’s one-to-one chat requests.
- Modifies a user’s message content, for example, by filtering out sensitive words or adding custom information defined by the app.

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding protocol for this callback. For more information on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and muting is returned for the callback before sending one-to-one chat messages, the callback after sending one-to-one chat messages cannot be triggered.
- If the callback before sending one-to-one chat messages and the callback after sending one-to-one chat messages are both enabled and the message body is modified during the callback before sending one-to-one chat messages, the callback after sending one-to-one chat messages will use the modified message for callback.
- For more security considerations, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a one-to-one chat message on the client.
- The app admin sends a one-to-one chat message by calling the RESTful SendMsg API.

## Callback Trigger Conditions

The IM backend has received a one-to-one chat message sent by a user but has not delivered the message to the target user.

## API Call Description

### Sample request URL

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**
```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | Specifies that the request protocol is HTTPS and the request method is POST. |
| [www.example.com](http://www.example.com) | Callback URL |
| SdkAppid | The SDKAppID assigned via the IM console when the application is created. |
| CallbackCommand | The value is fixed to C2C.CallbackBeforeSendMsg. |
| contenttype | The value is fixed to JSON in the request packet body. |
| ClientIP | The IP address of the client, such as 127.0.0.1. |
| OptPlatform | The platform of the client. For more information on the value, see the parameter description of the OptPlatform in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request packets

```
{
    "CallbackCommand": "C2C.CallbackBeforeSendMsg", // The callback command that is run.
    "From_Account": "jared", // The sender of the message.
    "To_Account": "Jonh", // The recipient of the message.
    "MsgSeq": 48374, // The sequence number of the message.
    "MsgRandom": 2837546, // The random number of the message.
    "MsgTime": 1557481126, // The timestamp indicating when the message was sent. Unit: seconds. 
    "MsgKey": "48374_2837546_1557481126", // The unique identifier of the message. It is used by RESTful APIs to recall a one-to-one chat message.
    "MsgBody": [ // The body of the message. For more information, see the TIMMessage message object.
        {
            "MsgType": "TIMTextElem", // The text of the message.
            "MsgContent": {}
                "Text": "red packet"
            }
        }
    ]
}
```

### Request packet fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | The callback command that is run. |
| From_Account | String | The UserID of the message sender. |
| To_Account | String | The UserID of the message recipient. |
| MsgSeq | Integer | The message sequence number, and the unique UserID of a message.<br>Group messages are sorted using MsgTime. The message with a larger MsgSeq value appears later.|
| MsgRandom | Integer | The random number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgTime | Integer | The message sending timestamp in seconds<br>One-to-one messages sent in the same second are sorted using MsgTime. The message with a larger MsgSeq value appears later. |
| MsgKey | String | The unique identifier of the message. It is used for [Recalling a One-to-One Chat Message by using RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/35015). |
| MsgBody | Array | The body of the message. For more information, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response packet when chatting is allowed

In the following example, the user is allowed to chat and the IM backend does not modify the content of the to-be-delivered message.

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0 // The value 0 indicates that chatting is allowed.
}
```

### Sample response packet when muting is enabled

In the following example, the user is muted. In this case, the IM backend does not deliver the to-be-delivered message, but returns error code `20006` to the message sender.

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 1 // The value 1 indicates that the user is muted.
}
```

### Sample response packet when the message content is modified

In the following example, the one-to-one chat message sent by the user is modified by adding custom information. In this case, the IM backend delivers the modified message. Based on this feature, the app backend can add special content such as the user level and title to the messages sent by users.
**Example:**

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0, // The parameter must be set to 0 so that the IM backend can deliver the modified message normally.
    "MsgBody": [ // The message modified by the app backend. If the app backend does not modify the message, the message sent by the user is used by default.
        {
            "MsgType": "TIMTextElem", // The text of the message.
            "MsgContent": {}
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // The custom information added to the message.
            "MsgContent": {}
                "Desc": " CustomElement.MemberLevel ", // The description of the message.
                "Data": " LV1" // The data of the message.
            }
        }
    ]
}
```

### Response packet fields

| Field | Type | Property | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The processing result of the request. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code returned for the request. 0: not muted. 1: muted. If the business team wants to mute a user and sends ErrorCode and ErrorInfo to the client, ensure that the value of ErrorCode is set within the range of [120001, 130000]. |
| ErrorInfo | String | Required | Detailed information on the error.|
| MsgBody | Array | Optional | The message body modified by the app backend. The IM backend sends the modified message to the user’s friend in the one-to-one chat. For more information on the format, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Invoke a Callback After Sending One-to-One Chat Messages] (https://intl.cloud.tencent.com/document/product/1047/34365)
- RESTful API: [Sending a One-to-One Chat Message](https://intl.cloud.tencent.com/document/product/1047/34919)
- RESTful API: [Batch Sending One-to-One Chat Messages](https://intl.cloud.tencent.com/document/product/1047/34920)

