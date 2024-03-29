## Feature Overview
- This API is used to update the relationship chain data of multiple friends of a user at a time.
- You are advised to update multiple friends of a user at a time to avoid write conflicts caused by concurrent writes.

## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/sns/friend_update?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters
The following table describes the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<br><li>China: `console.tim.qq.com`</li><li>Singapore: `adminapisgp.im.qcloud.com`</li><li>Seoul: `adminapikr.im.qcloud.com`</li><li>Frankfurt: `adminapiger.im.qcloud.com`</li><li>Mumbai: `adminapiind.im.qcloud.com`</li><li>Silicon Valley: `adminapiusa.im.qcloud.com`</li> |
| v4/sns/friend_update | Request API. |
| sdkappid | SDKAppID assigned by the Chat console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295. |
| contenttype |Request format, which should always be `json`. |

### Maximum call frequency

200 calls per second

### Sample request
- **Basic format**
```
{
    "From_Account":"id",
    "UpdateItem":
    [
        {
            "To_Account":"id1",
            "SnsItem":
            [
                {
                    "Tag":"Tag_SNS_IM_Remark",
                    "Value":"remark1"
                }
            ]
        }
    ]
}
```
- **Response to a complete request**
```
{
    "From_Account":"id",
    "UpdateItem":
    [
        {
            "To_Account":"id1",
            "SnsItem":
            [
                {
                    "Tag":"Tag_SNS_IM_Remark",
                    "Value":"remark1"
                },
                {
                    "Tag":"Tag_SNS_IM_Group",
                    "Value":
                    [
                        "group1",
                        "group2"
                    ]
                },
                {
                    "Tag":"Tag_SNS_Custom_Test",
                    "Value":"test"
                }
            ]
        }
    ]
}
```
- **Response to a batch request**
```
{
    "From_Account":"id",
    "UpdateItem":
    [
        {
            "To_Account":"id1",
            "SnsItem":
            [
                {
                    "Tag":"Tag_SNS_IM_Remark",
                    "Value":"remark1"
                }
            ]
        },
        {
            "To_Account":"id2",
            "SnsItem":
            [
                {
                    "Tag":"Tag_SNS_IM_Remark",
                    "Value":"remark2"
                },
                {
                    "Tag":"Tag_SNS_IM_Group",
                    "Value":
                    [
                        "group1",
                        "group2"
                    ]
                }
            ]
        },
        {
            "To_Account":"id3",
            "SnsItem":
            [
                {
                    "Tag":"Tag_SNS_IM_Remark",
                    "Value":"remark3"
                },
                {
                    "Tag":"Tag_SNS_IM_Group",
                    "Value":
                    [
                        "group3"
                    ]
                },
                {
                    "Tag":"Tag_SNS_Custom_Test",
                    "Value":"test"
                }
            ]
        }
    ]
}
```

### Request fields

| Field | Type | Required | Description |
|-----|-----|----|-----|
| From_Account | String | Yes | `UserID` of the account for which to update relationship chain data. |
| UpdateItem | Array | Yes | An object array of friends to be updated. |
| To_Account | String | Yes | `UserID` of a friend. |
| SnsItem  | Array | Yes | An object array of the relationship chain data to be updated. |
| Tag | String | Yes | The name of a relationship chain field to be updated. Users are only allowed to update the remarks, group, and custom fields of relationship chain. For more information on relationship chain fields, see the **Friend Lists** in <a href="https://intl.cloud.tencent.com/document/product/1047/33521">Relationship Chain Management</a>. |
| Value | Array/String/Integer | Yes | The value of a relationship chain field. For information on value types, see the **Friend Lists** section in <a href="https://intl.cloud.tencent.com/document/product/1047/33521">Relationship Chain Management</a>. |

### Sample response
- **Response to a basic or complete request**
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
- **Response to a batch request**
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
			"ResultCode":30011,
			"ResultInfo":"Err_SNS_FriendUpdate_Group_Num_Exceed_Threshold"
		},
		{
			"To_Account":"id3",
			"ResultCode":30002,
			"ResultInfo":"Err_SNS_FriendImport_SdkAppId_Illegal"
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

|Field|Type|Description|
|------|-----|------|
| ResultItem | Array | The result of updating friends, which is an array of UserIDs and corresponding results. |
| To_Account | String | `UserID` of the friend that you requested to update. |
| ResultCode | Integer | The result of `To_Account`. `0`: Successful. Other values: Failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | The error description of `To_Account`. This field is empty if the request succeeds. |
| Fail_Account | Array | The users that failed to be verified. This field is only returned when at least one user fails. |
| ActionStatus | String | Request result. `OK`: Successful. `FAIL`: Failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information. |
| ErrorDisplay | String | Detailed information displayed on the client |

[](id:ErrorCode)
## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30002 | The SDKAppID does not match. |
| 30003 | The requested account does not exist. |
| 30004 | The request requires app admin permissions. |
| 30006 | Internal server error. Try again. |
| 30007 | Network timeout. Try again later. |
| 30008 | A write conflict occurred due to concurrent write operations. You are advised to use bulk processing. |
| 30011 | The maximum number of friend lists has been reached. |

## API Debugging Tool
Use the [RESTful API online debugging tool](https://tcc.tencentcs.com/im-api-tool/index.html#/v4/sns/friend_update) to debug this API.

## Reference
- Adding Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Deleting Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34905">v4/sns/friend_delete</a>)
- Deleting All Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Verifying Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34907">v4/sns/friend_check</a>)
- Pulling Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Pulling Specified Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)



