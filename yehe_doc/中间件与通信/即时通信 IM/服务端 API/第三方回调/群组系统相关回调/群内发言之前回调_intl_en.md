## Feature Description

This API is used by the app backend to monitor users' group messages in real time, including:
- Records group messages in real time, for example, by recording a log or synchronizing the messages to other systems.
- Blocks users' requests to send messages in a group.
- Modifies users' message content, for example, by filtering out sensitive words or adding custom information defined by the app.

## Notes

- To enable this callback, you must configure a callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a group message on the client.
- The app admin sends a group message via a RESTful API call.

## Callback Trigger Time

The callback is triggered before the IM backend sends a group message to group members.

## API Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | The request protocol is HTTPS and the request method is POST. |
| www.example.com | Callback URL |
| SdkAppid | SDKAppID assigned in the IM console when the app is created |
| CallbackCommand | The value is always `Group.CallbackBeforeSendMsg`. |
| contenttype | The value is always `JSON`. |
| ClientIP | IP address of the client, such as `127.0.0.1` |
| OptPlatform | Platform of the client. For more information about valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.
    "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent": {
                "Text": "red packet"
            }
        }
    ]
}
```

### Request fields

| Field | Type | Description |
| --- | --- | --- |
| CallbackCommand | String | Callback command |
| GroupId | String | ID of the group that generates group messages |
| Type | String | Type of the group that generates group messages, such as `Public`. For details, see [Group Types](https://intl.cloud.tencent.com/document/product/1047/33529). |
| From_Account | String | UserID of the message sender |
| Operator_Account | String | UserID of the request initiator, based on which the system can identify whether the request is initiated by the admin. |
| Random | Integer | A 32-bit random number in the request |
|OnlineOnlyFlag|Integer|The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.|
| MsgBody | Array | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response

#### Allowing group message sending

The user is allowed to send group messages, and the content of the message is not modified.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // The value `0` indicates the user is allowed to send group messages.
}
```

#### Forbidding group message sending

The user is not allowed to send group messages. In this case, the message is not sent, and the error code `10016` is returned to the caller.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // The value `1` indicates that the user is not allowed to send group messages.
}
```

#### Discarding messages silently

The user is not allowed to send group messages. In this case, the message is not sent, but a success message will be returned to the caller.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 2 // The value `2` indicates the message is silently discarded.
}
```

#### Modifying message content

In the following response sample, the group message sent by the user is modified (a custom message is added), and the IM backend will send the modified message. With this feature, the app backend can add special content, such as the user level and title, to the message sent by the user.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // This field must be set to `0` so that the modified message can be sent normally.
    "MsgBody": [ // Message modified by the app backend. If the app backend does not modify the message, the message sent by the user is used by default.
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

### Response fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request processing result. `OK`: successful; `FAIL`: failed. |
| ErrorCode | Integer | Yes | Error code returned. `0`: allows group message sending; `1`: forbids group message sending; `2`: discards the message silently. If the business side wants to forbid a user to send group messages and send` ErrorCode` and `ErrorInfo` to the client, ensure that the value of `ErrorCode` is set within the range of [10100, 10200]. |
| ErrorInfo | String | Yes | Error information |
| MsgBody | Array | No | Message body modified by the app backend. The IM backend sends the modified message to the group. For more information on the format, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)

