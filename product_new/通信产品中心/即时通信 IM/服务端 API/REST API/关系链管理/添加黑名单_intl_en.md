## API Description

This API is used to add someone to your blacklist. You can do this one by one or in batches.
>
>- If users A and B are friends, either one adding the other to the blacklist removes them from each other’s friend list.
> If user A blacklists user B, or vice versa, then neither of them can send a friend request to the other person.
>- If user B is on user A’s blacklist and user A is also on user B’s blacklist, then user A and B cannot establish a chat session.
-> If user B is on user A’s blacklist, but user A is not on user B’s blacklist, then user A can message user B but not the other way around.

## Input Parameters

### Sample request URL
```
https://console.tim.qq.com/v4/sns/black_list_add?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Parameters

The following is a list of the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/sns/black_list_add  | Request API |
| sdkappid | The SDKAppID is assigned by the IM console when the app is created. |
| identifier | The administrator account of the app. For more information, refer to [App Administrator](https://cloud.tencent.com/document/product/269/31999#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | A signature generated from the app administrator account. For details on how to generate the signature, refer to [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-digit integer ranging from 0 to 4294967295. |

### Maximum calling frequency

200/second

### Sample request

```
{
	"From_Account":"id",
	"To_Account":["id1","id2","id3"]
}
```

### Request field descriptions

| Field | Type | Property | Description |
|--- |--- |--- |--- |
| From_Account | String | Required | The UserID that initiated the blacklist request. |
| To_Account | Array | Required | A list of UserIDs to be added to the blacklist. This array should not contain more than 1000 UserIDs. |

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

### Response field descriptions

| Field | Type | Description |
|--- |--- |--- |
| ResultItem | Array | The result of batch blacklisting, which is an array of UserIDs and corresponding results. |
| To_Account | String | The UserID that initiated the blacklist request. |
| ResultCode | Integer | The result of blacklisting. `0` means success and other values mean failure. For details on non-zero results, refer to [Error Codes](#ErrorCode). |
| ResultInfo | String | Error description. This field is empty when the request succeeds. |
| Fail_Account | Array | A list of users that failed to be added to the blacklist. This field is only returned when at least one user fails. |
| ActionStatus | String | Request result. `OK` means the request is successfully handled. `FAIL` means the request failed. |
| ErrorCode | Integer | Error code. `0` means success and other values mean failure. For details on non-zero results, refer to [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information. |
| ErrorDisplay | String | Detailed information displayed on the client. |

<span id="ErrorCode"></span>
## Error Codes
An HTTP status code 200 means the request was successfully received. The result of the blacklist operation is in the response, with details provided in fields such as `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`. An HTTP status other than 200, such as 502, means the request was not received.
For public error codes (60000 to 79999), refer to [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following are error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30002 | The SDKAppID does not match. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app administrator permissions. |
| 30006 | Internal server error. Please try again. |
| 30007 | Request timed out. Please try again later. |
| 30008 | A write conflict has occurred due to concurrent write operations. We recommend that you use batch processing. |
| 30013 | The maximum number of blacklisted users has been reached. |


## Testing
Use our [RESTful API Tester](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/sns/black_list_add) to test your requests.

## See Also

- Deleting a user from the blacklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34912">v4/sns/black_list_delete</a>)
- Querying a blacklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34914">v4/sns/black_list_get</a>)
- Verifying a blacklist (<a href="https://intl.cloud.tencent.com/document/product/1047/34913">v4/sns/black_list_check</a>)

## Callback

<td><a href="https://intl.cloud.tencent.com/document/product/1047/34361">Callback after adding a blacklist</a></td>
