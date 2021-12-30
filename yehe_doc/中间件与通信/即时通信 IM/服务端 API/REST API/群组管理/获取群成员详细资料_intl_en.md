## Feature Description
 This API is used by the app admin to obtain group member profiles based on the group ID.


## API Calling Description
### Applicable group types

| Group Type ID | RESTful API Support |
|-----------|------------|
| Private | Yes. Same as work group (Work) in the new version. |
| Public | Yes |
| ChatRoom | Yes. Same as meeting group (Meeting) in the new version. |
| AVChatRoom | Yes, but only the profiles of the first 300 members. |

Above are the IM built-in groups. For more information, see [Group system](https://intl.cloud.tencent.com/document/product/1047/33529).

>?Due to differences in scenario implementation, for an audio-video group (AVChatRoom), you can only obtain the group member profiles of the first 300 members. The profiles of members who join the group after the threshold (300) is reached cannot be obtained.

### Sample request URL
```
https://xxxxxx/v4/group_open_http_svc/get_group_member_info?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```



### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/group_open_http_svc/get_group_member_info | Request API |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum calling frequency
200 calls per second
### Sample requests

- **Basic format**
A basic request is used to obtain detailed group member information, including group member profiles and custom group member fields. The request requires only the group ID.
```
{
    "GroupId":"@TGS#1NVTZEAE4"  // Group ID (required)
}
```
- **Pagination**
You can use the `Limit` and `Offset` fields to control the pagination mode:
 - `Limit`: specifies the maximum number of members in the `MemberList` array in the response. Maximum value: 200; recommended value: 100
 - `Offset`: specifies from which group member to start pulling information. If the page number starts from `1`, the value of `Offset` for each page should be `(page number – 1) × number of group members to display on each page`.
 For example, to display 20 group members on each page, the request parameters for the first page should be `{"Limit": 20, "Offset": 0}`, the request parameters for the second page should be `{"Limit": 20, "Offset": 20}`, and so on.


```
{
    "GroupId":"@TGS#1NVTZEAE4", // Group ID (required)
    "Limit": 100, // Maximum number of members to pull information
    "Offset": 0 // Sequence number of the member from whom to start pulling information
}
```
- **Specifying information to pull**
You can use the `MemberInfoFilter` filter field to specify fields to pull. Fields that are not specified in it will not be pulled.
```
{
    "GroupId":"@TGS#1NVTZEAE4", // Group ID (required)
    "MemberInfoFilter": [ // Information to pull, where `Member_Account` is included by default. If this field is not specified, all group member information will be pulled.
        "Role",
        "JoinTime",
        "MsgSeq",
        "MsgFlag",
        "LastSendMsgTime",
        "ShutUpUntil",
        "NameCard"
    ]
}
```
- **Pulling the information of members in the specified role**
You can use the `MemberRoleFilter` filter field to specify the role of members to pull information. If this field is not specified, the information of members in all roles will be pulled.
```
{
    "GroupId":"@TGS#37AB3PAEC", // Group ID (required)
    "MemberRoleFilter":[ // Member role filter
        "Owner",
        "Member"
    ]
}
```
- **Pulling custom group member fields**
You can use the `AppDefinedDataFilter_GroupMember` filter field to specify the custom group member fields to pull. Fields that are not specified in it will not be pulled.
```
{
    "GroupId":"@TGS#37AB3PAEC", // Group ID (required)
    "AppDefinedDataFilter_GroupMember": [ // Filter for custom group member fields
        "MemberDefined2" // Key of a custom group member field
    ]
}
```
- **ALL IN ONE**
```
{
    "GroupId":"@TGS#1NVTZEAE4", // Group ID (required)
    "MemberInfoFilter": [ // Information to pull. If this field is not specified, all group member information will be pulled.
        "Role",
        "JoinTime",
        "MsgSeq",
        "MsgFlag",
        "LastSendMsgTime",
        "ShutUpUntil",
        "NameCard"
    ],
   "MemberRoleFilter":[ // Member role filter
        "Owner",
        "Member"
    ],
   "AppDefinedDataFilter_GroupMember": [ // Filter for custom group member fields
        "MemberDefined2", // Key of a custom group member field
        "MemberDefined1"
    ],
    "Limit": 100, // Maximum number of members to pull information
    "Offset": 0 // Sequence number of the member from whom to start pulling information
}
```

### Request fields

| Field | Type | Required | Description |
|---------|---------|---------|---------|
| GroupId | String | Yes | ID of the group to pull member information |
| MemberInfoFilter | Array | No | Information to pull. If this field is not specified, all group member information will be pulled. For details on group member information fields, see the **Group member profile** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E8.B5.84.E6.96.99). |
| MemberRoleFilter | Array | No | Role of group members to pull information. If this field is not specified, the information of members in all roles will be pulled. The member role can be `Owner`, `Admin`, or `Member`.  |
| AppDefinedDataFilter_GroupMember | Array | No | This field is omitted by default. It specifies the custom group member fields to pull. For more information, see the **Custom Fields** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |
| Limit | Integer | No | Maximum number of members to pull information at a time. The value cannot exceed 6000. If this field is not specified, the information of all members in the group will be obtained. |
| Offset | Integer | No | Sequence number of the member from whom to start pulling information. If this field is set to `0`, the information is pulled starting from the first member. |

### Sample responses
- **Response to a basic or pagination request**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MemberNum": 2, // Total number of members in the group
    "MemberList": [ // Group member list
        {
            "Member_Account": "bob",
            "Role": "Owner",
            "JoinTime": 1425976500, // Time when the member joined the group
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500, // Last time when the member sent a message
            "ShutUpUntil": 1431069882, // Muting end time in seconds
            "AppMemberDefinedData": [ // Custom group member fields
                {
                   "Key": "MemberDefined1",
                   "Value": "ModifyDefined1"
                },
                {
                    "Key": "MemberDefined2",
                    "Value": "ModifyDefined2"
                }
             ]
        },
        {
            "Member_Account": "peter",
            "Role": "Member ",
            "JoinTime": 1425976500,
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500,
            "ShutUpUntil": 0, // `0`: the member is not muted; other values: the time when the member will be unmuted
            "AppMemberDefinedData": [ // Custom group member fields
                {
                   "Key": "MemberDefined1",
                   "Value": "ModifyDefined1"
                },
                {
                    "Key": "MemberDefined2",
                    "Value": "ModifyDefined2"
                }
             ]
        }
    ]
}
```
- **Response to a request pulling specified fields**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MemberNum": 2, // Total number of members in the group
    "MemberList": [ // Group member list
        {
            "Member_Account": "bob",
            "Role": "Owner",
            "JoinTime": 1425976500, // Time when the member joined the group
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500, // Last time when the member sent a message
            "ShutUpUntil": 1431069882, // Muting end time in seconds
        },
        {
            "Member_Account": "peter",
            "Role": "Member ",
            "JoinTime": 1425976500,
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500,
            "ShutUpUntil": 0, // `0`: the member is not muted; other values: the time when the member will be unmuted
        }
    ]
}
```
- **Response to request pulling the information of members in the specified role**
```
{
    "ActionStatus": "OK", // The request succeeded.
    "ErrorCode": 0, // Return code
    "MemberList": [
        {
            "JoinTime": 1450680436, // Time when the member joined the group
            "LastSendMsgTime": 0, // Last time when the member sent a message
            "Member_Account": "Test_1", // Member account
            "MsgFlag": "AcceptNotNotify", // Type of member messages being blocked
            "MsgSeq": 1, // Sequence number of the member’s read message
            "NameCard": "", // Member’s contact card
            "Role": "Owner", // Member’s role
            "ShutUpUntil": 0 // `0`: the member is not muted; other values: the time when the member will be unmuted
        },
        {
            "JoinTime": 1450680436,
            "LastSendMsgTime": 0,
            "Member_Account": "Test_6",
            "MsgFlag": "AcceptNotNotify",
            "MsgSeq": 1,
            "NameCard": "",
            "Role": "Admin",
            "ShutUpUntil": 0
        }
    ],
    "MemberNum": 8 // Total number of members in the group
}
```
- **Response to a request pulling custom group member fields**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MemberNum": 2, // Total number of members in the group
    "MemberList": [ // Group member list
        {
            "Member_Account": "bob",
            "Role": "Owner",
            "JoinTime": 1425976500, // Time when the member joined the group
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500, // Last time when the member sent a message
            "ShutUpUntil": 1431069882, // Muting end time in seconds
             "AppMemberDefinedData": [ // Custom group member fields
                {
                    "Key": "MemberDefined2",
                    "Value": "ModifyDefined2"
                }
             ]
        },
        {
            "Member_Account": "peter",
            "Role": "Member",
            "JoinTime": 1425976500,
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500,
            "ShutUpUntil": 0, // `0`: the member is not muted; other values: the time when the member will be unmuted
            "AppMemberDefinedData": [ // Custom group member fields
                {
                    "Key": "MemberDefined2",
                    "Value": "ModifyDefined2"
                }
             ]
        }
    ]
}
```
- **Response to an ALL IN ONE request**
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "MemberNum": 2, // Total number of members in the group
    "MemberList": [ // Group member list
        {
            "Member_Account": "bob",
            "Role": "Owner",
            "JoinTime": 1425976500, // Time when the member joined the group
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500, // Last time when the member sent a message
            "ShutUpUntil": 1431069882, // Muting end time in seconds
            "AppMemberDefinedData":[ // Custom group member fields
                {
                   "Key":"MemberDefined1",
                   "Value":"ModifyDefined1"
                },
                {
                    "Key":"MemberDefined2",
                    "Value":"ModifyDefined2"
                }
             ]
        },
        {
            "Member_Account": "peter",
            "Role": "Member",
            "JoinTime": 1425976500,
            "MsgSeq": 1233,
            "MsgFlag": "AcceptAndNotify",
            "LastSendMsgTime": 1425976500,
            "ShutUpUntil": 0, // `0`: the member is not muted; other values: the time when the member will be unmuted
            "AppMemberDefinedData": [ // Custom group member fields
                {
                   "Key": "MemberDefined1",
                   "Value": "ModifyDefined1"
                },
                {
                    "Key": "MemberDefined2",
                    "Value": "ModifyDefined2"
                }
             ]
        }
    ]
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information |
| MemberNum | Integer | Total number of members in the group |
| MemberList | Array | Returned group member list, which contains information of all or specified group members. For details on group member information fields, see the **Group member profile** section in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529#.E7.BE.A4.E6.88.90.E5.91.98.E8.B5.84.E6.96.99). |
| AppMemberDefinedData | Array | Returned custom group member fields |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 10002 | Internal server error. Try again. |
| 10003 | Invalid command word. |
| 10004 | Invalid parameter. Check the error description and troubleshoot the issue. |
| 10007  | No operation permissions. Check whether the operator is an app admin or whether the operator has the permission to read the fields in the request. |
| 10010 | The group does not exist or has been deleted. |
| 10015 | Invalid group ID. Use the correct group ID. |
| 10018  | The response exceeds the maximum size allowed (1 MB) because the group member data volume is too large. Try to use `Limit` and `Offset` to pull the group member data by page. |


## API Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/group_open_http_svc/get_group_member_info) to debug this API.

## Reference
Modifying the Profile of a Group Member ([v4/group_open_http_svc/modify_group_member_info](https://intl.cloud.tencent.com/document/product/1047/34900))
