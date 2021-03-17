## Feature Description

This API is used by the app backend to monitor users' one-to-one messages in real time, including:
- Records one-to-one messages in real time, for example, by recording a log or synchronizing the messages to other systems.
- Collects statistics on one-to-one messages, for example, in terms of the number of users or the number of messages.

## Notes:

- To enable this callback, you must configure the callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and forbidding message sending is returned for the callback before sending one-to-one messages, the callback after sending one-to-one messages cannot be triggered.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and the message body is modified during the callback before sending one-to-one messages, the callback after sending one-to-one messages will use the modified message for callback.
- For more security considerations, see the **Security Considerations** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a one-to-one message on the client.
- The app admin sends a one-to-one message by calling the `sendmsg` RESTful API.

## Callback Trigger Time

The callback is triggered after the IM backend receives a one-to-one message sent by a user and sends the message to the target user.

>!If the IM backend fails to send the message, for example, due to sensitive word filtering, the callback is still triggered.

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
| CallbackCommand | The value is always `C2C.CallbackAfterSendMsg`. |
| contenttype | The value is always `JSON`. |
| ClientIP | IP address of the client, such as `127.0.0.1` |
| OptPlatform | Platform of the client. For more information about valid values, see the parameter description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request packet

```
{
    "CallbackCommand": "C2C.CallbackAfterSendMsg", // Callback command
    "From_Account": "jared", // Sender
    "To_Account": "Jonh", // Recipient
    "MsgSeq": 48374, // Sequence number of the message
    "MsgRandom": 2837546, // Random number of the message
    "MsgTime": 1557481126, // Timestamp in seconds indicating when the message is sent 
    "MsgKey": "48374_2837546_1557481126", // Unique identifier of the message. It is used by RESTful APIs to recall the one-to-one message.
    "SendMsgResult": 0, // Message sending result
    "ErrorInfo": "send msg succeed", // Error information related to the failure to send the message. If the message is sent successfully, the value of this field is `send msg succeed`.
    "UnreadMsgNum": 7, // Total number of unread one-to-one messages of `To_Account`
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
| CallbackCommand | String | Callback command |
| From_Account | String | UserID of the message sender |
| To_Account | String | UserID of the message recipient |
| MsgSeq | Integer | Sequence number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgRandom | Integer | Random number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgTime | Integer | Timestamp in seconds indicating when the message is sent. <br>One-to-one messages are preferentially sorted by `MsgTime`. Messages sent in the same second are sorted by `MsgSeq`. Messages with larger values of `MsgSeq` are after those with smaller values of `MsgSeq`. |
| MsgKey | String | Unique identifier of the message. It can be used to [recall the message](https://intl.cloud.tencent.com/document/product/1047/35015) via a RESTful API call. |
| SendMsgResult | Integer | Message sending result. `0`: successful; other values: failed. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |
| ErrorInfo | String | Error information related to the failure to send the message. If the message is sent successfully, the value of this field is `send msg succeed`. |
| UnreadMsgNum | Integer | Total number of unread one-to-one messages of `To_Account` (including all one-to-one chats). If the message fails to be sent, for example, due to sensitive word filtering, the value of this field is `-1`.|
| MsgBody | Array | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // `0`: callback succeeds; `1`: an error occurs during callback.
}
```

### Response packet fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request processing result. `OK`: successful; `FAIL`: failed. |
| ErrorCode | Integer | Yes | Error code. `0`: callback succeeds; `1`: an error occurs during callback. |
| ErrorInfo | String | Yes | Error information |

References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback Before Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34364)
- RESTful API: [Sending One-to-One Messages to One User](https://intl.cloud.tencent.com/document/product/1047/34919)
- RESTful API: [Sending One-to-One Messages to Multiple Users](https://intl.cloud.tencent.com/document/product/1047/34920)
