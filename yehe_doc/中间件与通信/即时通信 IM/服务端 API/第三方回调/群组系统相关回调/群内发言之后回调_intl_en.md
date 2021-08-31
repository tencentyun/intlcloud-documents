## Feature Description

This API is used by the app backend to monitor users' group messages in real time. The app backend can be notified when a group message is sent successfully and can synchronize the data as required.

## Notes

- To enable this callback, you must configure a callback URL and enable the corresponding switch for this callback. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Trigger Scenarios

- An app user sends a group message on the client.
- The app admin sends a group message via a RESTful API call.

## Callback Trigger Time

The callback is triggered after a group message is sent successfully.

## API Call Description

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
| CallbackCommand | The value is always `Group.CallbackAfterSendMsg`. |
| contenttype | The value is always `JSON`. |
| ClientIP | IP address of the client, such as `127.0.0.1` |
| OptPlatform | Platform of the client. For more information about valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand": "Group.CallbackAfterSendMsg", // Callback command
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
| MsgSeq | Integer | Message sequence number, which uniquely identifies a message<br>Group messages are sorted by `MsgSeq`. The larger the `MsgSeq` value, the lower a message ranks. |
| MsgTime | Integer | Message sending timestamp, corresponding to the backend server time |
|OnlineOnlyFlag|Integer|The value is `1` if it is an online message and `0` (default) if it’s not. For audio-video groups, the value is `0`.|
| MsgBody | Array | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response

A response is sent after the app backend synchronizes the data.

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //The value `0` indicates that the callback result is ignored.
}
```

### Response fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| ActionStatus | String | Yes | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Yes | Error code. The value `0` indicates that the callback result is ignored. |
| ErrorInfo | String | Yes | Error information |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Sending Ordinary Messages in a Group](https://intl.cloud.tencent.com/document/product/1047/34959)

