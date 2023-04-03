## Feature Overview

This webhook event is used by the app backend to check users' group messages in real time. The app backend can be notified when a group message is sent successfully and can synchronize the data as required.

## Limits

- To enable this webhook, you must configure a callback URL and enable the corresponding switch for this webhook. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- An app user sends a group message on the client.
- The app admin sends a group message via RESTful APIs.

## Webhook Triggering Timing

The webhook is triggered after a group message is sent successfully.

## API Calling Description

### Sample request URL

In the following sample, the webhook URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Webhook URL                                                  |
| SdkAppid        | The `SDKAppID` assigned by the Chat console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterSendMsg`.                   |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample requests

```
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // Webhook command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
    "MsgSeq": 123, // Sequence number of the message
    "MsgTime": 1490686222, // Time of the message
    "OnlineOnlyFlag": 1, // The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.
    "MsgBody": [ // Message body. For more information, see the `TIMMessage` message object.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent":{
                "Text": "red packet"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data",
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field            | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | Webhook command                                              |
| GroupId          | String  | ID of the group that generates group messages                |
| Type             | String  | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| From_Account     | String  | `UserID` of the message sender                               |
| Operator_Account | String  | `UserID` of the request initiator, based on which the system can identify whether the request is initiated by the admin. |
| Random           | Integer | A 32-bit random number in the request                        |
| MsgSeq           | Integer | Message sequence number, which uniquely identifies a message<br>Group messages are sorted by `MsgSeq`. The larger the `MsgSeq` value, the lower a message ranks. |
| MsgTime          | Integer | Message sending timestamp, corresponding to the backend server time |
| OnlineOnlyFlag   | Integer | The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`. |
| MsgBody          | Array   | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData  | String  | Custom message data. It is saved in the cloud and will be sent to the receiver. Such data can be pulled after the app is uninstalled and reinstalled. |
| TopicId          | String  | Topic ID, which indicates message sending in the topic and applies only to topic-enabled communities. |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

A response is sent after the app backend synchronizes the data.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //The value `0` indicates that the webhook result is ignored.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates that the webhook result is ignored. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)
