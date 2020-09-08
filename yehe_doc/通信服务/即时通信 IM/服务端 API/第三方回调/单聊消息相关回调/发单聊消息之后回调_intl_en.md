## Features

This API is used by the app backend to monitor a user’s one-to-one chat messages in real time, including:
- Records one-to-one messages in real time, for example, by recording a log or synchronizing the messages to other systems.
- Collects statistics on one-to-one messages, for example, in terms of the number of users or the number of messages.

## Notes

- To enable this callback, you must configure the callback URL and enable the corresponding protocol for this callback. For more information on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTPS POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is the SDKAppID of the app.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and muting is returned for the callback before sending one-to-one messages, the callback after sending one-to-one messages cannot be triggered.
- If the callback before sending one-to-one messages and the callback after sending one-to-one messages are both enabled and the message body is modified during the callback before sending one-to-one messages, the callback after sending one-to-one messages will use the modified message for callback.
- For more security considerations, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a one-to-one message on the client.
- The app admin sends a one-to-one message by calling the RESTful SendMsg API.

## Callback Trigger Conditions

The IM backend receives a one-to-one message sent by a user and delivers the message to the target user.

>! If the IM backend fails to deliver the message, for example, due to dirty word filtering, the callback is still triggered.

## API Description

### Sample request URL

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Sample:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter | Description |
| --- | --- |
| https | Specifies that the request protocol is HTTPS and the request method is POST. |
| www.example.com | The callback URL. |
| SdkAppid | The SDKAppID assigned in the IM console when the app is created. |
| CallbackCommand | The value is fixedly set to C2C.CallbackAfterSendMsg. |
| contenttype | Fixed value: JSON |
| ClientIP | The IP address of the client, such as 127.0.0.1. |
| OptPlatform | The platform of the client. For more information about possible values, see the parameter description of the OptPlatform in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request packet

```
{
    "CallbackCommand": "C2C.CallbackAfterSendMsg", // The callback command that is run.
    "From_Account": "jared", // The sender of the message.
    "To_Account": "Jonh", // The recipient of the message.
    "MsgSeq": 48374, // The sequence number of the message.
    "MsgRandom": 2837546, // The random number of the message.
    "MsgTime": 1557481126, // The timestamp indicating when the message was sent. Unit: seconds. 
    "MsgKey": "48374_2837546_1557481126", // The unique identifier of the message. It is used by RESTful APIs to recall a one-to-one message.
    "SendMsgResult": 0, //The message delivery result.
    "ErrorInfo": "send msg succeed", //The error information related to the failure to deliver the message. If the message is sent successfully, the content here is "send msg succeed".
    "MsgBody": [ // The body of the message.
        {
            "MsgType": "TIMTextElem", // The text of the message.
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
| From_Account | String | The UserID of the message sender. |
| To_Account | String | The UserID of the message recipient. |
| MsgSeq | Integer | The sequence number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgRandom | Integer | The random number of the message. It is used to identify the message and the value is a random 32-bit unsigned integer. |
| MsgTime | Integer | The timestamp indicating when the message was sent. Unit: seconds. <br>One-to-one messages are preferentially sorted by MsgTime. Messages sent in the same second are sorted by MsgSeq. Messages with larger MsgSeq values are placed after those with smaller values. |
| MsgKey | String | The unique identifier of the message. It is used for [Recalling a One-to-One Message by using RESTful APIs](https://intl.cloud.tencent.com/document/product/1047/35015). |
| SendMsgResult | Integer | The message delivery result. 0: delivered successfully. Other values: failed to deliver. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |
| ErrorInfo | String | The error information related to the failure to deliver the message. If the message is sent successfully, the content here is "send msg succeed". |
| MsgBody | Array | The body of the message. For more information, see [Message Format Description](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response packet

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0 // 0: callback succeeded. 1: an error occurred to callback.
}
```

### Response packet fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Required | The request processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | Required | The error code returned for the request. 0: callback succeeded. 1: an error occurred during callback. |
| ErrorInfo | String | Required | The error information. |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- [Callback before sending one-to-one messages](https://intl.cloud.tencent.com/document/product/1047/34364)
- RESTful API: [Sending a One-to-One Message](https://intl.cloud.tencent.com/document/product/1047/34919)
- RESTful API: [Batch Sending One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/34920)
