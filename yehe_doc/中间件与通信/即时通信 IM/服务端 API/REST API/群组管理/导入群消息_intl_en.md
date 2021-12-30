## Feature Description 
- This API is used to import group messages without triggering callbacks or sending notifications.
- When you are migrating your app from another instant messaging system to Tencent Cloud IM, you can use this API to import group message data.

## API Calling Description
### Applicable group types

| Group Type ID | Support for This RESTful API |
|-----------|------------|
| Private | Yes. Same as work group (Work) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as meeting groups (Meeting) in the new version. |
| AVChatRoom | No |

Above are the IM built-in groups. For more information, please see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Audio-video groups (AVChatRoom) do not support importing group messages. If you attempt to import group messages for these groups, error 10007 will be returned. Therefore, members of an audio-video group cannot view the messages sent before they join the group.


### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/import_group_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters
The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/import_group_msg | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum calling frequency

200 calls per second

### Sample request packet

A single request can import up to seven group messages.
After messages are imported through this API, the unread message count for all members will become `0`. To retain the unread message count, you need to import group members or set the unread message count for members after importing all messages.
The messages must be imported in ascending order by timestamp, and the timestamps of imported messages must be earlier than the current time, and later than the group creation time and the creation time of the latest message in the group. Otherwise, the import will fail.

```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "MsgList": [
        {
            "From_Account": "leckie", // Specified message sender
            "SendTime":1620808101,
            "Random": 8912345, // Random number of the message (optional)
            "MsgBody": [ // Message body, which consists of an element array. For details, see the `TIMMessage` message object.
                {
                    "MsgType": "TIMTextElem", // Text
                    "MsgContent": {
                        "Text": "red packet"
                    }
                },
                {
                    "MsgType": "TIMFaceElem", // Emoji
                    "MsgContent": {
                        "Index": 6,
                        "Data": "abc\u0000\u0001"
                    }
                }
            ]
        },
        {
            "From_Account": "peter", // Specified message sender
            "SendTime":1620892821,
            "MsgBody": [ // Message body, which consists of an element array. For details, see the `TIMMessage` message object.
                {
                    "MsgType": "TIMTextElem", // Text
                    "MsgContent": {
                        "Text": "red packet"
                    }
                }
            ]
        }

    ]
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the group for which to import messages |
| MsgList | String | Yes | List of the messages to import  |
| From_Account | String | Yes | Message sender |
| SendTime | Integer | Yes | Message sending time |
| Random | Integer | No | A 32-bit random number. If the random numbers of two messages within five minutes are the same, the later message will be discarded as a repeated message. |
| MsgBody | Object | Yes | TIM message. For more information, see the definition of `TIMMsgElement` in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |
| MsgType | String | Yes | TIM message object type. Valid values: `TIMTextElem` (text message), `TIMFaceElem` (emoji message), `TIMLocationElem` (location message), `TIMCustomElem` (custom message) |
| MsgContent | Object | Yes | TIM message object. For more information, see the definition of `TIMMsgElement` in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "ImportMsgResult": [
        {
            "MsgSeq": 1,
            "MsgTime": 1620808101,
            "Result": 0
        },
        {
            "MsgSeq": 2,
            "MsgTime": 1620892821,
            "Result": 0
        },
    ]
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorInfo | String | Error information |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ImportMsgResult | Array | Message import result |
| Result | Integer | Result of each message <ul><li>`0`: the message was imported successfully. </li><li>`10004`: the sending time of the message is invalid. </li><li>`80001`: the message contains restricted words and therefore cannot be stored. </li><li>`80002`: the message content exceeds the limit of 8,000 bytes. Please adjust the message size. |
| MsgTime | Integer | Message timestamp   |
| MsgSeq | Integer | Message sequence number, the unique identifier of a message |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. For example, a common member in a public group tries to remove other users from the group, but only the app admin can do so. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | The group ID is invalid. Use the correct group ID. |
| 10020 | The message is too large. Currently, the maximum message size supported is 8,000 bytes. Adjust the message size. |


## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/import_group_msg) to debug this API.

## Reference
Setting the Unread Message Count of a Member ([v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909))
