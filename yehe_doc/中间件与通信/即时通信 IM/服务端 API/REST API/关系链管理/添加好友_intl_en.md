## API Description
This API is used to add one or multiple users to the friend list.

## API Call Description
### Sample request URL
```
https://xxxxxx/v4/sns/friend_add?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters
The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/sns/friend_add | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created. |
| identifier | The administrator account of the app. For more information, see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is always `json`. |


### Maximum call frequency

200 calls per second

### Sample request
- **Simple request**
```
{
    "From_Account":"id",
    "AddFriendItem":
    [
        {
            "To_Account":"id1",
            "AddSource":"AddSource_Type_XXXXXXXX"
        }
    ]
}
```

- **Complete request**
```
{
    "From_Account":"id",
    "AddFriendItem":
    [
        {
            "To_Account":"id1",
            "Remark":"remark1",
            "GroupName":"Classmates", // Each user can only be assigned to one friend list when the user is added as a friend. Therefore, we can use `String` as the data type.
            "AddSource":"AddSource_Type_XXXXXXXX",
            "AddWording":"I'm Test1"
        }
    ],
    "AddType":"Add_Type_Both",
    "ForceAddFlags":1
}
```
- **Batch request**
```
{
    "From_Account":"id",
    "AddFriendItem":
    [
        {
            "To_Account":"id1",
            "AddSource":"AddSource_Type_XXXXXXXX"
        },
        {
            "To_Account":"id2",
            "Remark":"remark2",
            "GroupName":"Classmates", // Each user can only be assigned to one friend list when the user is added as a friend. Therefore, we can use `String` as the data type.
            "AddSource":"AddSource_Type_XXXXXXXX",
            "AddWording":"I'm Test2"
        },
        {
            "To_Account":"id3",
            "Remark":"remark3",
            "GroupName":"Colleagues", // Each user can only be assigned to one friend list when the user is added as a friend. Therefore, we can use `String` as the data type.
            "AddSource":"AddSource_Type_XXXXXXXX",
            "AddWording":"I'm Test3"
        }
    ],
    "AddType":"Add_Type_Both",
    "ForceAddFlags":1
}
```

### Request fields

| Field | Type | Required | Description |
|--- |--- |--- |--- |
| From_Account | String | Yes | The UserID that initiates the request. |
| AddFriendItem | Array | Yes | An array of friend objects. |
| To_Account | String | Yes | The UserID to add as a friend. |
| Remark | String | No | The name that the user who initiates the friend request writes about the user to be added. For details, refer to [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.87.E9.85.8D.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5). |
| GroupName | String | No | The group that the user who initiates the friend request assigns to the user to be added. Each user can only be assigned to one group. Therefore, we can use the `String` data type. For details, see the standard friend fields section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.87.E9.85.8D.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5). |
| AddSource | String | Yes | Source of the friend request. For details, see the standard friend fields section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.87.E9.85.8D.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5). |
| AddWording | String | No | Remarks that the user who initiates the friend request writes about the user to be added. For details, see the standard friend fields section in [Relationship Chain Management](https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.87.E9.85.8D.E5.A5.BD.E5.8F.8B.E5.AD.97.E6.AE.B5). |
| AddType | String | No | Friend adding type: <br><li>Add_Type_Single: one-sided <br><li>Add_Type_Both (default): mutual |
| ForceAddFlags | Integer | No | Flag denoting the friend is force added by an administrator: 1 means force added while 0 means the friend is added normally. |


### Sample response
- Response to **simple requests and complete requests**
```
{
	"ResultItem":
	[
		{
			"To_Account":"id1",
			"ResultCode":0,
			"ResultInfo":""
		}
	],
	"ActionStatus":"OK",
	"ErrorCode":0,
	"ErrorInfo":"",
	"ErrorDisplay":""
}
```

- Response to **batch requests**
```
{
	"ResultItem":
	[
		{
			"To_Account":"id1",
			"ResultCode":0,
			"ResultInfo":""
		},
		{
			"To_Account":"id2",
			"ResultCode":30006,
			"ResultInfo":"Err_SNS_FriendAdd_Unpack_Profile_Data_Fail"
		},
		{
			"To_Account":"id3",
			"ResultCode":30002,
			"ResultInfo":"Err_SNS_FriendAdd_SdkAppId_Illegal"
		}
	],
	"Fail_Account":["id2","id3"],
	"ActionStatus":"OK",
	"ErrorCode":0,
	"ErrorInfo":"",
	"ErrorDisplay":""
}
```

### Response fields

| Field | Type | Description |
|--- |--- |--- |
| ResultItem | Array | The result of adding friends in bulk, which is an array of UserIDs and corresponding results.|
| To_Account | String | The UserID that you requested to add as a friend. |
| ResultCode | Integer | Result of the friend request. `0` means the request was successful. Any non-zero value means the request failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | Error description. This field is empty when the request succeeds. |
| Fail_Account | Array | A list of users that failed to be added as friends. This field is only returned when at least one user fails. |
| ActionStatus | String | The result of the request. `OK` means the request was successful. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means the request was successful. Any non-zero value means the request failed. For detailed information on non-zero ResultCode values, refer to [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information. |
| ErrorDisplay | String | Detailed information displayed on the client. |

<span id="ErrorCode"></span>
## Error Codes

Unless a network error (such as error 502) occurs, the returned HTTP status code for this API is always 200. The specific error code and details can be found in the response fields such as `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The list below contains only error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Wrong request parameter. Check your request according to the error description. |
| 30002 | The SDKAppID does not match. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app administrator permissions. |
| 30005 | The relationship chain field contains sensitive words. |
| 30006 | Internal server error. Please try again. |
| 30007 | Request timed out. Please try again later. |
| 30008 | A write conflict has occurred due to concurrent write operations. We recommend that you use batch processing. |
| 30009 | You have been prohibited from adding friends. |
| 30010 | Your friend list is full. |
| 30011 | You have too many friend lists. |
| 30012 | You have too many pending friend requests. |
| 30014 | The user you are trying to add has too many friends. |
| 30515 | The user you are trying to add is on your blocklist. You cannot add this user. |
| 30516 | The user you are trying to add has disabled friend requests. |
| 30525 | You have been blocked by the user you are trying to add. You cannot add this user. |
| 30539 | The user you are trying to add has selected `AllowType_Type_NeeedConfirm` as their friend request authentication method. Your friend request is pending approval. This code is used to differentiate a successful friend request, meaning the friend is added, and a pending friend request, so more helpful messages can be displayed. |
| 30540 | You have sent too many friend requests in a short amount of time. Request filtered for security reasons. |

## API Debugging Tool
Use the [online RESTful API debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/sns/friend_add) to commission this API.

## See Also

- Importing friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34905">v4/sns/friend_delete</a>)
- Deleting all friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Verifying friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34907">v4/sns/friend_check</a>)
- Getting friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Getting specific friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)
