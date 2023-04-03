## Feature Overview

This callback allows you to monitor the exceptions on the application backend when group messages are sent, including:
- The message sent contains an incorrect parameter (for example, the group ID does not exist).
- The message sending frequency exceeds the limit.
- The message sent is found to be non-compliant after content filtering.
- The sender is muted.

## Notes

- To enable this callback, you must configure a callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user sends a group message on the client.
- The app admin sends a group message via a RESTful API call.

## Callback Triggering Timing

It will be triggered after the IM backend failed to deliver the group message to group members.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackSendMsgException`.               |
| contenttype     | Fixed value: `JSON`.                                         |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackSendMsgException", // Callback command
    "GroupId": "@TGS#2J4SZEAEL", // Group ID
    "Type": "Public", // Group type
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
    "ErrorCode": 10023, // Message exception error code
    "ErrorInfo": "msg count exceeds limit,please retry later" // Message exception details
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field            | Type     | Description                                                  |
| ---------------- | -------- | ------------------------------------------------------------ |
| CallbackCommand  | String   | Callback command                                             |
| GroupId          | String   | ID of the group that generates group messages                |
| Type             | String   | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| From_Account     | String   | `UserID` of the message sender                               |
| Operator_Account | String   | UserID of the request initiator, based on which the system can identify whether the request is initiated by the admin. |
| Random           | Integer  | A 32-bit random number in the request                        |
| OnlineOnlyFlag   | Integer  | The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`. |
| MsgBody          | Array    | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| CloudCustomData  | String   | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |
| ErrorCode        | Interger | Message exception error code. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348). |
| ErrorInfo        | String   | Message exception details                                    |
| EventTime        | Integer  | Event trigger timestamp in milliseconds                      |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response fields

| Field        | Type    | Required | Description                                  |
| ------------ | ------- | -------- | -------------------------------------------- |
| ActionStatus | String  | Required | Request result. Fixed value: `OK`.           |
| ErrorCode    | Integer | Required | Error code. Fixed value: `0`.                |
| ErrorInfo    | String  | Required | Error message. Fixed value: An empty string. |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)
