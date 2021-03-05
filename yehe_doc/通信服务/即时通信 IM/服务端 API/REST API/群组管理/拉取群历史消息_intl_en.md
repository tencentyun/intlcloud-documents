## Background

- IM group messages are sorted by their Seq values, which are assigned according to the order in which the server receives them. A group message sent earlier has a lower Seq number.
- When you pull all messages of a group for the first time, you do not need to specify a Seq for the operation. Instead, the server will automatically return the latest messages. When you pull messages of the group later, you need to set the Seq to a minimum of the last returned Seq minus 1.
- If `IsPlaceMsg` of the returned message is 1, the message with this Seq expired, failed to be stored, or was deleted.

## Feature Description

The app admin can pull historical messages of a group by calling this API.

## API Call Description
### Applicable group types

| Group Type ID | Support for This API |
|-----------|------------|
| Private | Yes. This group type is equivalent to Work (work group) in the new version. |
| Public | Yes. |
| ChatRoom | Yes. This group type is equivalent to Meeting (temporary meeting group) in the new version. |
| AVChatRoom | No. |

These are the native group types in IM. For more information, see the [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>? This API does not apply to AVChatRooms (live streaming groups) because AVChatRooms do not support the storage of historical messages.
### Sample request URL
```
https://console.tim.qq.com/v4/group_open_http_svc/group_msg_get_simple?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
 ```
### Request parameters

The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/group_open_http_svc/group_msg_get_simple | Request API |
| sdkappid | SDKAppID assigned by the IM console when the application is created |
| identifier | The administrator account of the app. For more information, refer to [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |


### Maximum call frequency

200 calls per second

### Sample request packet

- **Simple request**
This example shows how to pull the historical messages of a group, where the most recent `ReqMsgNumber` messages of the group are returned.
```
{
    "GroupId": "@TGS#15ERQPAER",    //ID of the group for which messages will be pulled
    "ReqMsgNumber": 2      //Number of messages to be pulled
}
```

- **Pulling by Seq**
This example shows how to pull historical messages of a group by Seq,
where `ReqMsgNumber` messages with a Seq number less than or equal to `ReqMsgSeq` are returned.
```
{
    "GroupId": "@TGS#15ERQPAER",
    "ReqMsgSeq": 7803321,       //Maximum Seq for messages to pull. Messages with a Seq number less than or equal to ReqMsgSeq are returned.
    "ReqMsgNumber": 2
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Required | ID of the group for which historical messages will be pulled |
| ReqMsgNumber | Integer | Required | Number of historical messages to pull. Currently, a maximum of 20 historical messages can be returned for one request. Therefore, we recommend that you set this field to less than or equal to 20. |
| ReqMsgSeq | Integer | Optional | Maximum Seq for messages to pull |

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
                        "Data": "\b\u0001\u0010\u0006\u001A\u0006猫瞳",
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
                        "Data": "\b\u0001\u0010\u0006\u001A\u000F西瓜妹妹。",
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
| ActionStatus | String | Request result. Valid values: `OK` for success and `FAIL` for failure |
| ErrorInfo| String | Error information |
| ErrorCode | Integer | Error code. Valid values: `0` for success and non-0 values for failure |
| GroupId | String | ID of the group in the request |
| IsFinished | Integer | Whether all messages within the requested range are returned. <li>If not all messages are returned because the message length is too long or too many (more than 20) messages are requested, the value is 0. </li><li>If the message length is too long or too many (more than 20) messages are requested but all messages have expired, the value is 2.</li> |
| RspMsgList | Array | List of returned messages |
| From_Account | String | Message sender |
| IsPlaceMsg | Integer | Whether the message is empty. If a message is deleted or has expired, `MsgBody` is empty, and the value of this field is 1. |
| MsgPriority | Integer | Message priority, which is used for message deduplication. This field is specified when the client sends a message. If it is not specified, it is generated automatically by the server. Valid values: `1` for high, `2` for normal, `3` for low, and `4` for lowest. |
| MsgRandom | Integer | Random value of a message, which is used for message deduplication. This field is specified when the client sends a message. If it is not specified, it is generated automatically by the server. |
| MsgSeq | Integer | Message Seq, which is used to uniquely identify a message. The smaller the value of this field, the earlier the message was sent. |
| MsgTimeStamp | Integer | Timestamp when the message was sent, which is the time on the server |
| MsgBody | Array | Message content. For more information, see the [Description of MsgBody Message Content](https://intl.cloud.tencent.com/document/product/1047/33527). |

## Error Codes

Unless a network error (such as error 502) occurs, the returned HTTP status code for this API is always 200. The specific error code and error information can be found in `ErrorCode` and `ErrorInfo` in the response packet.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The list below contains only error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | An internal server error occurred. Please try again. |
| 10003 | The command word is invalid. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | You have insufficient operation permissions. You must obtain the permissions necessary to perform this operation. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Make sure to use the correct group ID. |

## API Debugging Tool

This API can be debugged by using the [online debugging tool for RESTful APIs](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/group_open_http_svc/group_msg_get_simple).

## References
Configuring Unread Message Counts ([v4/group_open_http_svc/set_unread_msg_num)](https://intl.cloud.tencent.com/document/product/1047/34909))
