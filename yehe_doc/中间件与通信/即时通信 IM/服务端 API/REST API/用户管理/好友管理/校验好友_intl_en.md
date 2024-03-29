## Feature Overview
This API is used to check friendship in bulk.

## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/sns/friend_check?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<br><li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/sns/friend_check  | Request API |
| sdkappid | SDKAppID assigned by the Chat console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype |Request format, which should always be `json`. |

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

|Field|Type|Required|Description|
|-------|------|-------|-----|
| From_Account | String | Yes | The UserID of the account that requests to check friendship |
| To_Account | Array | Yes | The UserIDs of the friends to be checked. Each request cannot contain more than 1,000 UserIDs.|
|CheckType|String| Yes | Verification mode. For more information, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521">Verifying friends</a>. |

### Sample responses

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

|Field|Type|Description|
|------|------|-------|
| InfoItem|Array|The object array of verification results|
| To_Account|String| The UserID of the account that you requested to check |
| Relation|String|The friend relationship between `To_Account` and `From_Account` upon successful verification. For details, see <a href="https://intl.cloud.tencent.com/document/product/1047/33521">Verifying friends</a>.|
| ResultCode | Integer | The process result of `To_Account`. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | The error description of `To_Account`. This field is empty if the request succeeds. |
| Fail_Account | Array | The users that failed to be verified. This field is only returned when at least one user fails. |
| ActionStatus | String | The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information |
| ErrorDisplay | String | Detailed information displayed on the client |

[](id:ErrorCode)
## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30003 | The requested account does not exist. |
| 30004 | The request requires app admin permissions. |
| 30006 | Internal server error. Try again. |
| 30007 | Network timeout. Try again later. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#/v4/sns/friend_check) to debug this API.

## Reference
- Adding Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34905">v4/sns/friend_delete</a>)
- Deleting All Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Pulling Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Pulling Specified Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)

