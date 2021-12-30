## Feature Description
This API is used to verify friends in bulk.

## API Call Description
### Sample request URL
```
https://xxxxxx/v4/sns/friend_check?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/sns/friend_check  | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created |
| identifier | The administrator account of the app. For more information, please see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

200 calls per second

### Sample request
```
{
    "From_Account":"id",
    "To_Account":["id1","id2","id3","id4","id5"],
    "CheckType":"CheckResult_Type_Both"
}
```

### Request fields 

| Field | Type | Required | Description |
|-------|------|-------|-----|
| From_Account | String | Yes | The UserID of the account that requests to verify friends |
| To_Account | Array | Yes | The UserIDs of the friends to be verified. Each request cannot contain more than 1000 UserIDs.|
| CheckType | String | Yes | Verification mode. For details, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.A1.E9.AA.8C.E5.A5.BD.E5.8F.8B">Verifying Friends</a>. |

### Sample response

```
{
	"InfoItem": [
		{
			"To_Account": "id1",
			"Relation": "CheckResult_Type_BothWay",
			"ResultCode": 0,
			"ResultInfo": ""
		},
		{
			"To_Account": "id2",
			"Relation": "CheckResult_Type_AWithB",
			"ResultCode": 0,
			"ResultInfo": ""
		},
		{
			"To_Account": "id3",
			"Relation": "CheckResult_Type_BWithA",
			"ResultCode": 0,
			"ResultInfo": ""
		},
		{
			"To_Account": "id4",
			"Relation": "CheckResult_Type_NoRelation",
			"ResultCode": 0,
			"ResultInfo": ""
		},
		{
			"To_Account": "id5",
			"Relation": "CheckResult_Type_NoRelation",
			"ResultCode": 30006,
			"ResultInfo": "Err_SNS_FriendCheck_Check_Relation_Exec_Task_Fail"
		}
	],
	"Fail_Account": ["id5"],
	"ActionStatus": "OK",
	"ErrorCode": 0,
	"ErrorInfo": "",
	"ErrorDisplay": ""
}
```


### Response fields

| Field | Type | Description |
|------|------|-------|
| InfoItem|Array|The object array of verification results|
| To_Account|String| The UserID of the account that you requested to verify |
| Relation|String|The relationship between `To_Account` and `From_Account` upon successful verification. For details, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521#.E6.A0.A1.E9.AA.8C.E5.A5.BD.E5.8F.8B">Verifying Friends</a>.|
| ResultCode | Integer | The process result of `To_Account`. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | The error description of `To_Account`. This field is empty if the request succeeds. |
| Fail_Account | Array | The users that failed to be verified. This field is only returned when at least one user fails. |
| ActionStatus | String | The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information |
| ErrorDisplay | String | Detailed information displayed on the client |

<span id="ErrorCode"></span>
## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app administrator permissions. |
| 30006 | Internal server error. Please try again. |
| 30007 | Network timeout. Please try again later. |

## Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/sns/friend_check) to debug this API.

## References
- Adding Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34905">v4/sns/friend_delete</a>)
- Deleting All Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Pulling Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Pulling Specified Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)
