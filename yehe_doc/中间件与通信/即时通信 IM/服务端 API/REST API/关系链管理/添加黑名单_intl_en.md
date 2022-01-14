## API Description

This API is used to add one or multiple people to your blocklist.
>!
>- If users A and B are friends, either one adding the other to the blocklist removes them from each other’s friend list.
> If user A blocks user B, or vice versa, then neither of them can send a friend request to the other person.
>- If user B is on user A’s blocklist and user A is also on user B’s blocklist, then user A and B cannot start a conversation with each other.
-> If user B is on user A’s blocklist, but user A is not on user B’s blocklist, then user A can message user B but not the other way around.

## API Call Description

### Sample request URL
```
https://xxxxxx/v4/sns/black_list_add?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The list below contains only the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/sns/black_list_add  | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created. |
| identifier | The administrator account of the app. For more information, refer to [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample request

```
{
	"From_Account":"id",
	"To_Account":["id1","id2","id3"]
}
```

### Request fields

| Field | Type | Required | Description |
|--- |--- |--- |--- |
| From_Account | String | Yes | The UserID that initiates the blocklist request. |
| To_Account | Array | Yes | A list of UserIDs to be added to the blocklist. This array should not contain more than 1000 UserIDs. |

### Sample response

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
			"ResultCode":30001,
			"ResultInfo":"Err_SNS_BlackListAdd_Already_Exist"
		},
		{
			"To_Account":"id3",
			"ResultCode":30002,
			"ResultInfo":"Err_SNS_BlackListAdd_SdkAppId_Illegal"
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
| ResultItem | Array | The result of batch blocking, which is an array of UserIDs and corresponding results. |
| To_Account | String | The UserID that you requested to add to blocklist. |
| ResultCode | Integer | The result. `0` means success and other values mean failure. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | Error description. This field is empty when the request succeeds. |
| Fail_Account | Array | A list of users that failed to be added to the blocklist. This field is only returned when at least one user fails. |
| ActionStatus | String | The result of the request. `OK` means the request is successfully handled. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means success and other values mean failure. For details on non-zero results, see [Error Codes](#ErrorCode). |
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
| 30006 | Internal server error. Please try again. |
| 30007 | Request timed out. Please try again later. |
| 30008 | A write conflict has occurred due to concurrent write operations. We recommend that you use batch processing. |
| 30013 | The maximum number of blocked users has been reached. |


## API Debugging Tool
Use the [online RESTful API debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/sns/black_list_add) to commission this API.

## See Also

- Deleting a user from the blocklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34912">v4/sns/black_list_delete</a>)
- Querying a blocklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34914">v4/sns/black_list_get</a>)
- Verifying a blocklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34913">v4/sns/black_list_check</a>)

## Possible Callback

<td><a href="https://intl.cloud.tencent.com/document/product/1047/34361">Callback after adding users to the blocklist</a></td>
