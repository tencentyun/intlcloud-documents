## Background

- IM group messages are sorted by seq, and seq is allocated according to the order in which group messages are received by the server. The seq is greater for group messages sent earlier and smaller for group messages sent later.
- To pull all the messages of a group, you do not need to enter the seq for the initial pull. Instead, the server automatically returns the latest messages. For subsequent pulls, enter the previously returned smallest seq minus 1.
- If the value of `IsPlaceMsg` in the returned message is `1`, it indicates that the message with this seq has expired, failed to be stored, or been deleted.

## Feature Description

This API allows the app administrator to pull the historical messages of a group.

## API Call Description
### Applicable group types

| Group Type ID | Support for This RESTful API |
|-----------|------------|
| Private | Yes. Same as work groups (Work) in the new version. |
| Public | Yes. |
| ChatRoom | Yes. Same as meeting groups (Meeting) in the new version. |
| AVChatRoom | No. |

Above are the IM built-in groups. For more information, please see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Audio-video groups (AVChatRoom) do not support this API because the historical messages of this type of group cannot be stored.
### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/group_msg_get_simple?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/group_msg_get_simple | The request API |
| sdkappid | The SDKAppID assigned by the IM console when an application is created |
| identifier | The app administrator account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |


### Maximum call frequency

200 calls per second

### Sample request packets

- **Basic request**
Pulls the historical messages of a group. The most recent `ReqMsgNumber` group messages will be returned.
```
{
    "GroupId": "@TGS#15ERQPAER",    // The ID of the group of which messages are to be pulled
    "ReqMsgNumber": 2      // The number of messages to be pulled
}
```

- **Pulling by seq**
Pulls the historical messages of a group based on the specified seq.
The seq of the returned messages is less than or equal to the `ReqMsgNumber` of `ReqMsgSeq`.
```
{
    "GroupId": "@TGS#15ERQPAER",
    "ReqMsgSeq": 7803321,       // The maximum seq of the requested messages. The messages with a seq less than or equal to `ReqMsgSeq` will be returned.
    "ReqMsgNumber": 2
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group of which messages are to be pulled |
| ReqMsgNumber | Integer | Yes | The number of historical messages to be pulled. At present, a maximum of 20 historical messages can be returned per request. Therefore, please set the value of this field to 20 or less. |
| ReqMsgSeq | Integer | No | The maximum seq of the messages to be pulled |

### Sample response packet
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "GroupId": "@TGS#15ERQPAER",
    "IsFinished": 1,
    "RspMsgList": [
        {
            "From_Account": "144115197276518801",
            "IsPlaceMsg": 0,
            "MsgBody": [
                {
                    "MsgContent": {
                        "Data": "\b\u0001\u0010\u0006\u001A\u0006 MaoTong",
                        "Desc": "MIF",
                        "Ext": ""
                    },
                    "MsgType": "TIMCustomElem"
                },
                {
                    "MsgContent": {
                        "Data": "",
                        "Index": 15
                    },
                    "MsgType": "TIMFaceElem"
                }
            ],
            "MsgPriority": 1,
            "MsgRandom": 51083293,
            "MsgSeq": 7803321,
            "MsgTimeStamp": 1458721802
        },
        {
            "From_Account": "144115198339527735",
            "IsPlaceMsg": 0,
            "MsgBody": [
                {
                    "MsgContent": {
                        "Data": "\b\u0001\u0010\u0006\u001A\u000F Watermelon Girl",
                        "Desc": "MIF",
                        "Ext": ""
                    },
                    "MsgType": "TIMCustomElem"
                },
                {
                    "MsgContent": {
                        "Text": "Report"
                    },
                    "MsgType": "TIMTextElem"
                }
            ],
            "MsgPriority": 1,
            "MsgRandom": 235168582,
            "MsgSeq": 7803320,
            "MsgTimeStamp": 1458721797
        }
    ]
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorInfo | String | Error information |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. |
| `groupID` | `String` | The group ID in the request |
| IsFinished | Integer | Whether all the requested messages are returned.<li>If all the requested messages are returned, the value of this field is `1`.</li><li>If not all requested messages are returned because the messages are too long or the number of messages is greater than 20, the value of this field is `0`.</li><li>If the requested messages are too long or the number of messages is greater than 20 and all the messages have expired, the value of this field is `2`.</li> |
| MsgList | Array | A list of returned messages |
| From_Account | String | The UserID of the message sender |
| IsPlaceMsg | Integer | Whether a message is empty. If the message has been deleted or expired, `MsgBody` is empty and the value of this field is `1`. If the message has been recalled, the value of this field is `2`. |
| MsgPriority | Integer | Message priority, which is used for message deduplication. A value is entered when the client sends a message. If no value is entered, the server automatically generates one. `1`: high priority; `2`: normal priority, `3`: low priority; `4`: lowest priority |
| MsgRandom | Integer | Message random value, which is used for message deduplication. A value is entered when the client sends a message. If no value is entered, the server automatically generates one. |
| MsgSeq | Integer | The unique seq of the message. The smaller the value, the earlier the message was sent. |
| MsgTimeStamp | Integer | The timestamp when the message was sent, which follows the server time system |
| MsgBody | Array | Message body. For more information, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. The operator must have permissions to perform corresponding operations. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Make sure to use the correct group ID. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/group_msg_get_simple) to debug this API.

## Reference
Setting the Unread Message Count of a Member ([v4/group_open_http_svc/set_unread_msg_num](https://intl.cloud.tencent.com/document/product/1047/34909))
