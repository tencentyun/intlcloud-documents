>!This document is only for users who are migrating their apps to Tencent Cloud IM.
## Feature Description
- This API is used by app admins to set the unread message count of a group member. When this API is called, no callback is triggered and no notification is sent.
- When you are migrating your app from another IM system to Tencent Cloud IM, you can use this API to set the unread message count of group members.

## API Call Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as work group (Work) in the new version. |
| Public | Yes. |
| ChatRoom | No. Same as meeting group (Meeting) in the new version. |
| AVChatRoom | No. |
|Community|Yes.|

These are the built-in group types in IM. For detailed information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?ChatRoom and AVChatroom (audio-video) groups do not support unread message counts. Therefore, you cannot set an unread message count for members of these two group types. If you try to do so, no error will be returned.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/set_unread_msg_num?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters
The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/set_unread_msg_num | Request API |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency
200 calls per second
### Sample request packet

This example sets the unread message count of a specified group member.
If the unread message count specified by this API is greater than the current number of messages in the group, the unread message count will be set to the current number of messages in the group.
```
{
    "GroupId": "@TGS#2CLUZEAEJ",  // Target group (required)
    "Member_Account": "bob",  // Target group member (required)
    "UnreadMsgNum":5          // Unread message count of the target member
}
```

### Request packet fields 

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the target group |
| Member_Account | String | Yes | Target group member  |
| UnreadMsgNum | Integer | Yes | Unread message count of the target member |

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed. |
| ErrorInfo | String | Error information |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed. |


## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | No operation permissions. For example, a common member in a public group tries to remove other users from the group, but only the app admin can do so. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Make sure to use the correct group ID. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/set_unread_msg_num) to debug this API.

## Reference
Sending System Messages in a Group ([v4/group_open_http_svc/send_group_system_notification](https://intl.cloud.tencent.com/document/product/1047/34958))
