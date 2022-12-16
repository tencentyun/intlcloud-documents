## Feature Overview
- This API is used by the app admin to query the message history of a one-to-one conversation from the perspective of a party of the conversation based on a specified time range.
- The one-to-one conversation to be queried is specified by `Operator_Account` and `Peer_Account` in the request and the query is performed from the perspective of the party specified by `Operator_Account`. The query result contains the messages sent between both parties. The specific sender and recipient of each message are specified by `From_Account` and `To_Account` respectively.
- In most cases, the query result is the same if you perform the query from the perspective of either party of a one-to-one conversation. However, there are four cases where the results are different (some messages in the conversation can be queried by one party but not by the other party):
 - One party of the conversation has cleared the message history of the conversation by calling the terminal API [clearC2CHistoryMessage()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a29aa6e75c2238c35cc609bef0e5a46ce).
 - One party of the conversation has deleted the conversation by calling the terminal API [deleteConversation()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMConversationManager.html#a7a6e38c5a7431646bd4c0c4c66279077), web/mini program/uni-app API [deleteConversation](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteConversation), or [server API for deleting a conversation](https://intl.cloud.tencent.com/document/product/1047/43088) with `ClearRamble` being set to `1`.
 - One party of the conversation has deleted some messages in the conversation by calling the terminal API [deleteMessages()](https://im.sdk.qcloud.com/doc/zh-cn/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#adb346fede13d493e415f6574df911e9a) or web/mini program/uni-app API [deleteMessage](https://web.sdk.qcloud.com/im/doc/zh-cn/SDK.html#deleteMessage).
 - For messages sent through [the API for sending one-to-one messages to one user](https://intl.cloud.tencent.com/document/product/1047/34919) or [the API for sending one-to-one messages to multiple users](https://intl.cloud.tencent.com/document/product/1047/34920), `SyncOtherMachine` is set to `2`, indicating that specified messages are not synced to the message history of the other party of the conversation.
- The query result contains recalled messages indicated by the `MsgFlagBits` field.
- The `IsPeerRead` field in the query result indicates whether the recipient has sent the read receipt of this message. The value of this field becomes `1` only after the recipient calls [sendMessageReadReceipts (Android / iOS & Mac / Windows)](https://www.tencentcloud.com/document/product/1047/48022#.E6.8E.A5.E6.94.B6.E7.AB.AF.E5.8F.91.E9.80.81.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7) or [sendMessageReadReceipt (Web)](https://www.tencentcloud.com/document/product/1047/48021#.E6.8E.A5.E6.94.B6.E7.AB.AF.E5.8F.91.E9.80.81.E6.B6.88.E6.81.AF.E5.B7.B2.E8.AF.BB.E5.9B.9E.E6.89.A7).
- If you want to recall a message, you can first call this API to query the `MsgKey` of the message and then call the [RESTful API for recalling one-to-one messages](https://intl.cloud.tencent.com/document/product/1047/35015) to recall the message.
- The time range of message records that can be queried depends on the roaming message storage period, which is seven days by default. You can modify the message roaming period via the IM console. Extending the message roaming period is a value-added service. For more information, see [Message Storage](https://intl.cloud.tencent.com/document/product/1047/33524).
- If the total size of the messages within the requested time range exceeds the upper size limit (currently 13 KB) of the response, continued pulling is needed. You can see whether all the requested messages have been pulled by checking the `Complete` field in the response.

## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/openim/admin_getroammsg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters

The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>Chinese mainland: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com`<li>Silicon Valley: `adminapiusa.im.qcloud.com` |
| v4/openim/admin_getroammsg | Request API |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype |Request format, which should always be `json`. |

### Maximum call frequency

200 calls per second

### Sample requests and responses

For example, `user1` and `user2` had a conversation, and you want to query the conversation history from 2020-03-20 10:00:00 to 2020-03-20 11:00:00 from the perspective of user2.

#### Sample request
```
{
    "Operator_Account":"user2",
    "Peer_Account":"user1",
    "MaxCnt":100,
    "MinTime":1584669600,
    "MaxTime":1584673200
}
```
#### Sample response
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "Complete": 0,
    "MsgCnt": 12, //12 messages were returned for the pull.
    "LastMsgTime": 1584669680,
    "LastMsgKey": "549396494_2578554_1584669680",
    "MsgList": [
        {
            "From_Account": "user1",
            "To_Account": "user2",
            "MsgSeq": 549396494,
            "MsgRandom": 2578554,
            "MsgTimeStamp": 1584669680,
            "MsgFlagBits": 0,
            "IsPeerRead": 0,
            "MsgKey": "549396494_2578554_1584669680",
            "MsgBody":[
                {
                    "MsgType": "TIMTextElem",
                    "MsgContent":{
                        "Text": "msg 1"
                    }
                }
            ],
            "CloudCustomData": "your cloud custom data"
        },
        {
            "From_Account": "user2",
            "To_Account": "user1",
            "MsgSeq": 1054803289,
            "MsgRandom": 7201,
            "MsgTimeStamp": 1584669689,
            "MsgFlagBits": 0,
            "IsPeerRead": 0,
            "MsgKey": "1054803289_7201_1584669689",
            "MsgBody":[
                {
                    "MsgType": "TIMTextElem",
                    "MsgContent":{
                        "Text": "msg 2"
                    }
                }
            ],
            "CloudCustomData": "your cloud custom data"
        },
        { ... } // The remaining ten messages are not listed for simplicity.
    ]
}
```
In the response, `"Complete": 0` indicates that not all messages generated within the time range have been pulled. Therefore, continued pulling is required.
**In the continued pulling request, the value of `MaxTime` must be changed to the value of `LastMsgTime` in the response, and the `LastMsgKey` in the response must be entered**, as shown below:

##### Sample continued pulling request[](id:example)
```
{
    "Operator_Account":"user2",
    "Peer_Account":"user1",
    "MaxCnt":100,
    "MinTime":1584669600,
    "MaxTime":1584669680,
    "LastMsgKey": "549396494_2578554_1584669680"
}
```
#### Sample response
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "Complete": 1,
    "MsgCnt": 5, // Five messages were returned for the pull.
    "LastMsgTime": 1584669601,
    "LastMsgKey": "1456_23287_1584669601",
    "MsgList": [
        {
            "From_Account": "user1",
            "To_Account": "user2",
            "MsgSeq": 1456,
            "MsgRandom": 23287,
            "MsgTimeStamp": 1584669601,
            "MsgFlagBits": 0,
            "IsPeerRead": 1,
            "MsgKey": "1456_23287_1584669601",
            "MsgBody":[
                {
                    "MsgType": "TIMTextElem",
                    "MsgContent":{
                        "Text": "msg 13"
                    }
                }
            ],
            "CloudCustomData": "your cloud custom data"
        },
        {
            "From_Account": "user2",
            "To_Account": "user1",
            "MsgSeq": 9806,
            "MsgRandom": 14,
            "MsgTimeStamp": 1584669602,
            "MsgFlagBits": 0,
            "IsPeerRead": 1,
            "MsgKey": "9806_14_1584669602",
            "MsgBody":[
                {
                    "MsgType": "TIMTextElem",
                    "MsgContent":{
                        "Text": "msg 14"
                    }
                }
            ],
            "CloudCustomData": "your cloud custom data"
        },
        { ... } // The remaining three messages are not listed for simplicity.
    ]
}
```
In the response, `"Complete": 1` indicates that all messages generated within the time range have been pulled.
If the value of `Complete` in the response is `0`, you need to continue pulling messages until the value of `Complete` becomes `1`.

#### Request fields

| Field | Type | Required | Description |
|---------|---------|----|---------|
| Operator_Account | String | Yes | UserID of one party of the conversation for which messages are queried. The result may be different if you query messages for the other party of the same conversation. For more information, see the API description section. |
| Peer_Account | String | Yes | `UserID` of the other party in the conversation |
| MaxCnt | Integer | Yes | Number of messages to query |
| MinTime | Integer | Yes | Minimum value of the time range of the messages to query |
| MaxTime | Integer | Yes | Maximum value of the time range of the messages to query |
| LastMsgKey | String | No | `MsgKey` of the last message that was pulled previously. This field is required for continued pulling. For more information, see the preceding [sample](#example). |

### Sample response
- Response to a successful request
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "Complete": 1,
    "MsgCnt": 1,
    "LastMsgTime": 1584669680,
    "LastMsgKey": "549396494_2578554_1584669680",
    "MsgList": [
        {
            "From_Account": "user1",
            "To_Account": "user2",
            "MsgSeq": 549396494,
            "MsgRandom": 2578554,
            "MsgTimeStamp": 1584669680,
            "MsgFlagBits": 0,
            "IsPeerRead": 0,
            "MsgKey": "549396494_2578554_1584669680",
            "MsgBody":[
                {
                    "MsgType": "TIMTextElem",
                    "MsgContent":{
                        "Text": "1"
                    }
                }
            ],
            "CloudCustomData": "your cloud custom data"
        }
    ]
}
```

- Response to a failed request
```
{
    "ActionStatus": "FAIL", 
    "ErrorInfo": "Fail to Parse json data of body, Please check it", 
    "ErrorCode": 90001
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: Successful; `FAIL`: Failed |
| ErrorCode| Integer | Error code. `0`: Successful; other values: Failed |
| ErrorInfo| String | Error information |
| Complete | Integer | Whether all messages have been pulled. `0`: no, continued pulling is required; `1`: yes |
| MsgCnt | Integer | Number of messages that were pulled this time |
| LastMsgTime | Integer | Time when the last message was pulled this time |
| LastMsgKey | String | Identifier of the last message pulled this time |
| MsgList | Array | List of returned messages |
| MsgFlagBits | Integer | Message attribute. `0`: normal message; `8`: recalled message |
| IsPeerRead | Integer | Whether the recipient has sent the read receipt of this message. Valid values: `0` for no and `1` for yes. For details, see the feature description of this API.  |
| MsgBody | Array | Message body. For details on formats, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). (Note: A message can contain multiple message elements, in which case `MsgBody` is an array.) |
| CloudCustomData | String | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |
| MsgKey | String | Message identifier. You can use this field when calling the [RESTful API for recalling one-to-one messages](https://intl.cloud.tencent.com/document/product/1047/35015). |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 90001 | Failed to parse the JSON request. Make sure the format is valid. |
| 90003 | The `To_Account` field is missing in the JSON request or it is not a string. |
| 90008 | The `From_Account` field is missing in the JSON request or the account it specifies does not exist. |
| 90009 | The request requires app admin permissions. |
| 91000 | Internal service error. Try again. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US) to debug this API.

## References
- [Sending One-to-One Messages to One User](https://intl.cloud.tencent.com/document/product/1047/34919) (v4/openim/sendmsg)
- [Sending One-to-One Messages to Multiple Users](https://intl.cloud.tencent.com/document/product/1047/34920) (v4/openim/batchsendmsg)
- [Recalling One-to-One Messages](https://intl.cloud.tencent.com/document/product/1047/35015) (v4/openim/admin_msgwithdraw)
