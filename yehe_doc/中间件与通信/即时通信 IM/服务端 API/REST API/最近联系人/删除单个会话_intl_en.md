## Feature Description
This API is used to delete a conversation. It can also clear roaming messages.

## API Calling Description
### Sample request URL
```
https://xxxxxx/v4/recentcontact/delete?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https | The request protocol is HTTPS, and the request method is POST. |
| xxxxxx | Domain name corresponding to the country/region where your SDKAppID is located.<li>China: `console.tim.qq.com`<li>Singapore: `adminapisgp.im.qcloud.com`<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com` |
| v4/recentcontact/delete  | Request API                             |
| sdkappid | `SDKAppID` assigned by the IM console when an app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |

### Maximum call frequency

200 calls per second

### Sample request
```
{
	"From_Account":"id1",
	"Type":1,
	"To_Account":"id2",
	"ClearRamble":1
}
```

### Request fields

|Field|Type|Required|Description|
|-------|------|-------|-----|
|From_Account|String|Yes|`UserID` of the account for which to delete a conversation|
|Type|Integer|Yes|Conversation type. `1`: one-to-one conversation; `2`: group conversation |
|To_Account|String|Yes|`UserID` of the other user in the conversation to be deleted |
|ClearRamble|Integer|No|Whether to clear roaming messages. `1`: yes; `0`: no |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": "",
    "ErrorDisplay": ""
}
```


### Response fields

|Field|Type|Description|
|------|------|-------|
| ActionStatus | String | The request result. `OK`: successful. `FAIL`: failed. |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed. For details on non-zero results, please see [Error Codes](#ErrorCode). |
| ErrorInfo| String | Detailed error message |
| ErrorDisplay | String | Detailed information displayed on the client |

[](id:ErrorCode)
## Error Codes
The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ResultCode`, `ResultInfo`, `ErrorCode`, and `ErrorInfo`.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 50001  | The requested UserID has not been imported into the Tencent Cloud IM backend. Please import. |
| 50002  | Incorrect request parameter. Check your request according to the error description.                                    |
| 50003  | The request requires app admin permissions.                                      |
| 50004  | Internal server error. Please try again.                                      |
| 50005  | Network timeout. Try again later.                                       |

## API Debugging Tool
Use our [RESTful API Tester](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/recentcontact/delete) to test your requests.
