## Feature Overview

This webhook event is used by the app backend to check users' group messages in real time, including:
- Records group messages in real time, for example, by recording a log or synchronizing the messages to other systems.
- Blocks users' requests to send messages in a group.
>! The timeout period of the webhook before message sending is two seconds by default, and we recommend you not adjust it. This webhook may time out when used for text moderation. If you need to moderate text, use the content webhook. 

## Limits

- To enable this webhook, you must configure a webhook URL and enable the corresponding switch for this webhook. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- An app user sends a group message on the client.
- The app admin sends a group message via RESTful APIs.

## Webhook Triggering Timing

The webhook is triggered before the Chat backend sends a group message to group members.

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
| CallbackCommand | Fixed value: `Group.CallbackBeforeSendMsg`.                  |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Webhook Protocols** section of [Webhook Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample requests

```
{
    "CallbackCommand": "Group.CallbackBeforeSendMsg", // Webhook command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Community", // Group type
    "From_Account": "jared", // Sender
    "Operator_Account":"admin", // Request initiator
    "Random": 123456, // Random number
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
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// Topic ID, which applies only to topic-enabled communities
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
| OnlineOnlyFlag   | Integer | The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`. |
| MsgBody          | Array   | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData  | String  | Custom message data. It is saved in the cloud and will be sent to the receiver. Such data can be pulled after the app is uninstalled and reinstalled. |
| TopicId          | String  | Topic ID, which indicates message sending in the topic and applies only to topic-enabled communities. |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

#### Allowing group message sending

The user is allowed to send group messages, and the content of the message is not modified.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 // `0` indicates the user is allowed to send messages.
}
```

#### Forbidding group message sending

The user is not allowed to send group messages. In this case, the message is not sent, and the error code `10016` is returned to the caller.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 1 // `1` indicates that the user is not allowed to send messages.
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

#### Modifying the message content

In the following response sample, the group message sent by the user is modified (a custom message is added), and the Chat backend will send the modified message. With this feature, the app backend can add special content, such as the user level and title, to the message sent by the user.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0, // This field must be set to `0` so that the modified message can be sent normally.
    "MsgBody": [ // Message modified by the app backend. If the app backend does not modify the message, the message sent by the user is delivered.
        {
            "MsgType": "TIMTextElem", // Text
            "MsgContent":{
                "Text": "red packet"
            }
        },
        {
            "MsgType": "TIMCustomElem", // Custom message
            "MsgContent":{
                "Desc": "CustomElement.MemberLevel", // Description
                "Data": "LV1" // Data
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}
```

### Response fields

| Field           | Type    | Required | Description                                                  |
| --------------- | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus    | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode       | Integer | Yes      | Error code returned. `0`: allows group message sending; `1`: forbids group message sending; `2`: discards the message silently. If the business side wants to forbid a user to send group messages and send` ErrorCode` and `ErrorInfo` to the client, ensure that the value of `ErrorCode` is set within the range of [10100, 10200]. |
| ErrorInfo       | String  | Yes      | Error information                                            |
| MsgBody         | Array   | No       | Message body modified by the app backend. The Chat backend sends the modified message to the group. For more information on the format, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData | String  | No       | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |


## References

- [Webhook Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)
