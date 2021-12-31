## Feature Description
 This API allows the app administrator to add new members to a group.

## API Call Description
### Applicable group types

| Group Type ID | Support for This RESTful API |
|-----------|------------|
| Private | Yes. Same as work groups (Work) in the new version. |
| Public | Yes. |
| ChatRoom |Yes. Same as meeting groups (Meeting) in the new version.|
| AVChatRoom | No. |

Above are the IM built-in groups. For more information, please see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).

>!Audio-video groups (AVChatRoom) do not support this API. If you use this API on an audio-video group, error 10007 will be returned. The only way for users to join this type of group is to apply to join.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/add_group_member?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Introduction](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/add_group_member  | Request API |
| sdkappid | The SDKAppID assigned by the IM console when an application is created |
| identifier | The app administrator account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample request packets

- **Basic request**
Used to invite users to a group. A single request supports adding up to 300 members. By default, the backend delivers group system notifications to all group members, except for private groups (or work groups in the new version) that have not been activated.
```
{
    "GroupId": "@TGS#2J4SZEAEL", // The group to which to add members (required)
    "MemberList": [ // Up to 300 members can be added at a time.
    {
        "Member_Account": "tommy" // The ID of the member to be added (required)
    },
    {
        "Member_Account": "jared"
    }]
}
```

- **Adding members silently**
When `Silence` is set to `1`, the system does not notify anyone after successfully adding members.
```
{
    "GroupId": "@TGS#2J4SZEAEL", // The group to which to add members (required)
    "Silence": 1, // Whether to add members silently (optional)
    "MemberList": [ // Up to 300 members can be added at a time.
    {
        "Member_Account": "tommy" // The ID of the member to be added (required)
    },
    {
        "Member_Account": "jared"
    }]
}
```

### Request packet fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | The ID of the group to which to add members |
| Silence | Integer | Yes | Whether to add members silently. `0`: no. `1`: yes. The default value is `0`. |
| MemberList | Array | Yes | A list of the members to be added |
| Member_Account | String | Yes | The UserID of the member to be added  |

### Sample response packet
```
{
    "ActionStatus": "OK",
    "ErrorInfo":"",
    "ErrorCode": 0,
    "MemberList": [
    {
         "Member_Account": "tommy",
         "Result": 1 // The result of adding the member. 0: failed. 1: successful. 2: already in the group.
    },
    {
         "Member_Account": "jared",
         "Result": 1
    }]
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. |
| ErrorInfo | String | Error information |
| MemberList | Array | The result of adding members  |
| Member_Account | String | The UserID of the member |
| Result | Integer | The result of adding the member. `0`: failed. `1`: successful. `2`: already in the group. `3`: pending approval by the invitee. |

## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
|---------|---------|
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10005 | The number of member accounts in the request packet exceeds 300. |
| 10007 | No operation permissions. In this case, check whether the group type supports user invitation. For example, AVChatRoom and BChatRoom groups do not allow anyone to invite others to the groups. |
| 10014 | The users in the request cannot be added to the group because the group is already full. In this case, try deleting some `Member_Account` in the request or change the value of the `MaxMemberNum` field in the basic group information. For information, please see the **Basic group information** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E5.9F.BA.E7.A1.80.E8.B5.84.E6.96.99). |
| 10010 | The group does not exist or has been deleted. |
| 10015 | The group ID is invalid. Make sure to use the correct group ID. |
| 10016 | The developer backend has rejected this operation through a third-party callback. |
| 10019 | The UserID does not exist. Make sure all the accounts specified in `Member_Account` are correct. |
| 10026 | The command word of the `SDKAppID` request is disabled. Contact customer service. |
| 10037 | The number of groups that the invited user has joined exceeds the limit. In this case, check and delete the `Member_Account` that has joined excessive groups, or purchase an upgrade based on the your need. For information on IM plans, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350). |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/add_group_member) to debug this API.

## Reference
Deleting Group Members ([v4/group_open_http_svc/delete_group_member](https://intl.cloud.tencent.com/document/product/1047/34949))

## Possible Callbacks

- [Callback Before Accepting a Request to Add a User to a Group](https://intl.cloud.tencent.com/document/product/1047/34371)
- [Callback After a User Joins a Group](https://intl.cloud.tencent.com/document/product/1047/34372)
- [Callback After a Group Is Full](https://intl.cloud.tencent.com/document/product/1047/34376)
