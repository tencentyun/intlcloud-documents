## Feature Description
This API is used to delete friends. Both one-way deletion and two-way deletion are supported.

## API Call Description
### Sample request URL
```
https://xxxxxx/v4/sns/friend_delete?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` |
| v4/sns/friend_delete | Request API |
| sdkappid | The SDKAppID assigned by the IM console when the application is created |
| identifier | The administrator account of the app. For more information, please see [App Administrator](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated in the app administrator account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |


### Maximum call frequency

200 calls per second

### Sample requests
- **One-way deletion**
```
{
    "From_Account":"id",
    "To_Account":["id1","id2","id3"],
    "DeleteType":"Delete_Type_Single"
}
```
- **Two-way deletion**
```
{
    "From_Account":"id",
    "To_Account":["id1","id2","id3"],
    "DeleteType":"Delete_Type_Both"
}
```

### Request fields

| Field | Type | Required | Description |
|----|----|----|-----|
| From_Account | String | Yes | The UserID of the account that requests to delete friends |
| To_Account | Array | Yes | The list of UserIDs of the friends to be deleted. Each request cannot contain more than 1000 UserIDs. |
|  DeleteType | String  | No  | Deletion mode. For details, see [Deleting Friends](https://intl.cloud.tencent.com/document/product/1047/33521#.E5.88.A0.E9.99.A4.E5.A5.BD.E5.8F.8B).|

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
            "ResultCode":0,
            "ResultInfo":""
        },
        {
            "To_Account":"id3",
            "ResultCode":0,
            "ResultInfo":""
        }
    ],
    "ActionStatus":"OK",
    "ErrorCode":0,
    "ErrorInfo":"0",
    "ErrorDisplay":""
}
```

### Response fields

| Field | Type | Description |
|----|----|-----|
| ResultItem | Array | The result object array of deleting friends in bulk|
| To_Account|String| The UserID you requested to delete|
| ResultCode | Integer | The process result of `To_Account`. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ResultInfo | String | The error description of `To_Account`. This field is empty if the request succeeds. |
| ActionStatus | String | The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful. Other values: failed. For details on non-zero results, see [Error Codes](#ErrorCode). |
| ErrorInfo | String | Detailed error information |
| ErrorDisplay | String | Detailed information displayed on the client |

<span id="ErrorCode"></span>
## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | Incorrect request parameter. Check your request according to the error description. |
| 30002 | The SDKAppID does not match. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app administrator permissions. |
| 30006 | Internal server error. Please try again. |
| 30007 | Network timeout. Please try again later. |
| 30008 | A write conflict occurred due to concurrent write operations. You are advised to use bulk processing. |
| 31704 | The account you requested to delete is not your friend. |
| 31707 | The friend deletion request was filtered by the security policy. Do not initiate friend deletion requests too frequently. |

## Debugging Tool
Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/sns/friend_delete) to debug this API.

## References
- Adding Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting All Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Verifying Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34907">v4/sns/friend_check</a>)
- Pulling Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Pulling Specified Friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)

## Possible Callback

<a href="https://intl.cloud.tencent.com/document/product/1047/34360">Callback After Deleting Friends</a>
