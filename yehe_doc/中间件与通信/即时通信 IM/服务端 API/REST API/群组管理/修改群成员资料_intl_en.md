## Feature Description
 This API is used by the app admin to modify the profile of a group member.

## API Calling Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as Work (work group) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as the meeting group (Meeting) in the new version. |
| AVChatRoom | No. |
|Community|Yes.|

These are the built-in group types in IM. For detailed information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Audio-video groups do not store group member profiles and therefore do not allow member profile modification. They only support modifying the member profiles of admins and the group owner. Error 10007 will be returned if you try to modify the profiles of common group members.


### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/modify_group_member_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters
The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/modify_group_member_info | Request API. |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum call frequency

200 calls per second

### Sample requests
- **Set an admin**
Set a specified group member as an admin.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "Role": "Admin" // Set as an admin
}
```

- **Cancel an admin**
Revoke a specified group member's admin role.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "Role": "Member" //Cancel the admin role
}
```

- **Set a member's message blocking type**
Set a specified member's message blocking type, whose possible values are as follows. AcceptAndNotify: accept and notify. Discard: neither accept nor notify. AcceptNotNotify: accept but do not notify.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "MsgFlag": "AcceptAndNotify" // Message blocking type, which can be AcceptAndNotify, Discard, or AcceptNotNotify
}
```

- **Set a member's group name card**
Set a specified user's group name card, whose maximum length is 50 bytes.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "NameCard": "bob" // Group name card (optional)
}
```

- **Set member custom fields**
Set group member custom fields. By default, AppMemberDefinedData is not available and needs to be enabled in the [IM console](https://console.cloud.tencent.com/im) before use. For details, see the description table for request fields.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "AppMemberDefinedData": [ // Target member custom field (optional)
        {
            "Key":"MemberDefined1", // Key of the target group member custom field
            "Value":"ModifyData1" // Value of the key
        },
        {
            "Key":"MemberDefined3",
            "Value":"ModifyData3"
        }
    ]
}
```

- **Set a group member's muting period**
Set a specified group member's muting period.
```
{
    "GroupId": "@TGS#2CLUZEAEJ", // Target group (required)
    "Member_Account": "bob", // Target group member (required)
    "ShutUpTime":86400 // Muting period for the specified user, in seconds
}
```
Private groups (i.e., same as work groups in the new version) do not support muting members. 
### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Required | ID of the target group. |
| Member_Account | String | Required | Target group member.  |
| Role | String | Optional | Role of the member. Admin: set as an admin. Member: cancel the admin role.  |
| MsgFlag | String | Optional | Message blocking type.  |
| NameCard | String | Optional | Group name card (with a maximum length of 50 bytes).  |
| AppMemberDefinedData | Array | Optional | Group member custom field. By default, this field is not available and needs to be enabled in the [IM console](https://console.cloud.tencent.com/im). For details, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).  |
| ShutUpTime |Integer | Optional | Muting period in seconds. `0`: unmuted. |

### Sample response

```
{
    "ActionStatus":"OK",
    "ErrorInfo": "",
    "ErrorCode": 0
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. |
| ErrorInfo | String | Detailed error information |

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
| 10015 | Invalid group ID. Be sure to use the correct group ID. |
| 80001 | The modified group member information failed text content filtering. Check whether the modified group member information contains sensitive words. |

## Debugging Tool
Use the [online debugging tool for RESTful APIs](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/modify_group_member_info) to debug this API.

References
Obtaining detailed information on group members ([v4/group_open_http_svc/get_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34948))
