## API Description
 App administrators can use this API to push notifications to group chats.

## Input Parameters
### Applicable group types

| Group Type | Applicable |
|-----------|------------|
| Private group (Private) | Yes (supports push to specific members) |
| Public group (Public) | Yes (supports push to specific members) |
| Chatroom (ChatRoom) | Yes (supports push to specific members) |
| Audio and video chatroom (AVChatRoom) | Yes (all members only) |
| Broadcast Chatroom (BChatRoom) | Yes (all members only) |

These are the 5 native group types in IM. For detailed information, refer to [Brief Introduction to the Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

> Private groups, public groups, and chatrooms support pushing notifications to specific members, while audio and video chatrooms and broadcast chatrooms only support pushing notifications to all members.

### Sample request URL
```
https://console.tim.qq.com/v4/group_open_http_svc/send_group_system_notification?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Parameters

The following is a list of the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/group_open_http_svc/send_group_system_notification | Request API |
| sdkappid | The SDKAppID is assigned by the IM console when the app is created. |
| identifier  | The administrator account of the app. For more information, refer to [App Administrator](https://cloud.tencent.com/document/product/269/31999#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | A signature generated from the app administrator account. For details on how to generate the signature, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-digit integer ranging from 0 to 4294967295. |

### Maximum calling frequency

200/second

### Sample requests

- **To all members**
This pushes notifications to all members of a group.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "Content": "Hello World" // Content of the notification
}
```

- **To specific members**
This pushes notifications to only the specified members of a group, who are defined in ToMembers_Account. Audio and video groups and broadcast groups do not support this feature.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "ToMembers_Account": [ // List of notification recipients. Leave this empty to send notifications to all members.
        "peter",
        "leckie"
    ],
    "Content": "Hello World" // Content of the notification
}
```

### Request field descriptions

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group that is the target of the notification. |
| ToMembers_Account | Array | Yes | A list of recipients. Leave this empty to send notifications to all members. |
| Content | String | Yes | Content of the notification. |

### Sample response

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0
}
```

### Response field descriptions

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Status of the operation. `OK` means the request was successful. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means the operation was successful. Any non-zero value means the request failed. |
| ErrorInfo | String | Detailed error information. |

## Error Codes

An HTTP status code 200 means the request was successfully received. The result of the blacklist operation is in the response, with details provided in fields such as `ErrorCode` and `ErrorInfo`. An HTTP status other than 200, such as 502, means the request was not received.
For public error codes (60000 to 79999), refer to [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following are error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Server internal error. Please try again. |
| 10003 | Invalid request.                                               |
| 10004 | Invalid parameter. Use the error description to troubleshoot the issue. |
| 10007 | Insufficient permissions. For example, to remove someone from a public group requires administrator permissions. |
| 10010 | The group does not exist, or once existed but has been disbanded. |
| 10015 | Invalid GroupID. Make sure to use the correct GroupID. |

## Testing
Use our [RESTful API Tester](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/group_open_http_svc/send_group_system_notification) to test your requests.

## See Also
Sending ordinary messages in a group ([v4/group_open_http_svc/send_group_msg](https://cloud.tencent.com/document/product/269/1629))
