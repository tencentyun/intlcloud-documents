## Overview

This webhook event is used by the app backend to check the recalls of group messages in real time.

## Notes

- To enable this webhook, you must configure a webhook URL and toggle on the corresponding protocol. For more information on the configuration method, see [Webhook Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this webhook event, the Chat backend initiates an HTTP POST request to the app backend.
- After receiving the webhook request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Webhook Triggering Scenarios

- An app user recalls a group message on the client.
- An app admin recalls a group message via calling the RESTful API.

## Webhook Triggering Timing

After a group message is recalled successfully

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
| CallbackCommand | Fixed value: `Group.CallbackAfterRecallMsg`.                 |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Webhook Protocols** section of [Webhook Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
    "CallbackCommand":"Group.CallbackAfterRecallMsg", // Webhook command
    "Operator_Account":"admin", // Operator
    "Type": "Community", // Group type
    "GroupId":"1213456", // Group ID
    "MsgSeqList":[ // `MsgSeq` list of recalled messages           
        {"MsgSeq":130}
    ],
    "TopicId":"@TGS#_@TGS#cQVLVHIM62CJ@TOPIC#_TestTopic",// Topic ID, which applies only to topic-enabled communities
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Object           | Type    | Description                                                  |
| ---------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand  | String  | Webhook command                                              |
| Operator_Account | String  | The `UserID` of the operator who recalls a group message     |
| Type             | String  | Type of the group that generates group messages, such as `Public`. For details, see **Group Types** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| GroupId          | String  | Group ID                                                     |
| MsgSeqList       | Array   | `MsgSeq` list of recalled messages                           |
| TopicId          | String  | Topic ID, which indicates message recall in the topic and applies only to topic-enabled communities. |
| EventTime        | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

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
- Restful API: [Recalling Group Messages](https://intl.cloud.tencent.com/document/product/1047/34965)
