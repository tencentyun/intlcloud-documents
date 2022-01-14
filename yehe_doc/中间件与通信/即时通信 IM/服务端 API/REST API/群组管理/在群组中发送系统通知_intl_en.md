## Feature Description
 This API is used by app admins to push system notifications to group chats.

## API Call Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as work group (Work) in the new version. |
| Public | Yes. |
| ChatRoom | Yes. Same as meeting group (Meeting) in the new version. |
| AVChatRoom | Yes. But only to all group members.|

These are the built-in group types in IM. For detailed information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?A non-audio-video group supports sending system notifications to specified group members, but an audio-video group (AVChatRoom) only supports sending system notifications to all group members.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/send_group_system_notification?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/group_open_http_svc/send_group_system_notification | Request API |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample request packets

- **To all members**
This example pushes a system notification to all members in a group.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Content": "Hello World" // Content of the notification
}
```

- **To specific members**
To specify who can receive the system notification, set the recipients in `ToMembers_Account`. Audio-video groups (AVChatRoom) only support sending system notifications to all group members, but not specified group members.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "ToMembers_Account": [ // List of recipients. You can leave this field empty to send the notification to all members.
        "peter",
        "leckie"
    ],
    "Content": "Hello World" // Content of the notification
}
```

### Request packet fields 

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the group to which the notification will be sent |
| ToMembers_Account | Array | Yes | List of recipients. You can leave this field empty to send the notification to all members. |
| Content | String | Yes | Content of the notification |

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
| ErrorCode | Integer | Error code. `0`: successful; other values: failed. |
| ErrorInfo | String | Error information |

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
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/send_group_system_notification) to debug this API.

## Reference
Sending ordinary messages in a group ([v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959))
