## API Description
 App administrators can use this API to push notifications to group chats.

## API Call Description
### Applicable group types

| Group Type | Applicable |
|-----------|------------|
| Private group (Private) | Yes (supports push to specific members) |
| Public group (Public) | Yes (supports push to specific members) |
| Chat room (ChatRoom) | Yes (supports push to specific members) |
| Audio-video chat room (AVChatRoom) | Yes (all members only) |
| Broadcasting chat room (BChatRoom) | Yes (all members only) |

These are the 5 native group types in IM. For detailed information, see [here](https://intl.cloud.tencent.com/document/product/1047/33529).

> Private groups, public groups, and chat rooms support pushing notifications to specific members, while audio-video chat rooms and broadcasting chat rooms only support pushing notifications to all members.

### Sample request URL
```
https://console.tim.qq.com/v4/group_open_http_svc/send_group_system_notification?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/group_open_http_svc/send_group_system_notification | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created. |
| identifier  | The administrator account of the app. For more information, see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |

### Maximum call frequency

200 calls per second

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
This pushes notifications to only the specified members of a group, who are defined in ToMembers_Account. Audio-video chat rooms and broadcasting chat rooms do not support this feature.
```
{
    "GroupId": "@TGS#2C5SZEAEF",
    "ToMembers_Account": [ // List of notification recipients. Leave this field empty to send notifications to all members.
        "peter",
        "leckie"
    ],
    "Content": "Hello World" // Content of the notification
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group to which the notification will be sent. |
| ToMembers_Account | Array | Yes | A list of recipients. Leave this field empty to send notifications to all members. |
| Content | String | Yes | Content of the notification. |

### Sample response

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The result of the request. `OK` means the request was successful. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means the request was successful. Any non-zero value means the request failed. |
| ErrorInfo | String | Detailed error information. |

## Error Codes

Unless a network error (such as error 502) occurs, the returned HTTP status code for this API is always 200. The specific error code and details can be found in the response fields such as `ResultCode`, `ResultInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The list below contains only error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Please try again. |
| 10003 | Invalid command word.                                               |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007 | Insufficient permissions. For example, to remove someone from a public group requires administrator permissions. |
| 10010 | The group does not exist, or once existed but has been disbanded. |
| 10015 | Invalid group ID. Make sure to use the correct group ID. |

## API Debugging Tool
Use the [online RESTful API debugging tool](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/group_open_http_svc/send_group_system_notification) to commission this API.

## See Also
Sending ordinary messages in a group ([v4/group_open_http_svc/send_group_msg](https://intl.cloud.tencent.com/document/product/1047/34959))
