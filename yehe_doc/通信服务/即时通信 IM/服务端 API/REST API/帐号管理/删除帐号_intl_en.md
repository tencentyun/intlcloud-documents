## Feature Description 

- Only accounts of apps using the IM Trial plan can be deleted. Apps using other trial types such as TRTC, Whiteboard,Pro Edition and Flagship Edition do not support deleting accounts.
  >?You can log to the [console](https://console.cloud.tencent.com/im) and click an app to view its standard billing plan in **Basic Configuration** > **Standard Billing Plan** > **Plan**.
- When an account is deleted, the account’s data such as relationship chain and profile will also be deleted.
- After an account is deleted, **the account’s data cannot be recovered**. Therefore, exercise caution when using this API.

## API Calling Description

### Sample request URL

```
https://xxxxxx/v4/im_open_login_svc/account_import?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters

 The following table only describes the modified parameters when this API is called. For more information on other parameters, please see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ----------------------------------- | ------------------------------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com ` <li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`|
| v4/im_open_login_svc/account_delete | Request API |
| sdkappid | `SDKAppID` assigned by the console when the app is created |
| identifier | App admin account. For more information, please see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated in the app admin account. For details on how to generate the signature, please see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4294967295 |
| contenttype | Request format. The value is always `json`. |

### Maximum calling frequency

100 calls per second

### Sample request packet

```
{
  "DeleteItem":
  [
      {
          "UserID":"UserID_1"
      },
      {
          "UserID":"UserID_2"
      }
  ]
}
```

### Request packet fields

| Field | Type | Required | Description |
| ---------- | ------ | ---- | --------------------------------------------------- |
| DeleteItem | Array  | Yes | Account array to delete. A single request can contain up to 100 accounts. |
| UserID | String | Yes | `UserID` of the account to delete |

### Sample response packet

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": "",
    "ResultItem": [
        {
            "ResultCode": 0,
            "ResultInfo": "",
            "UserID": "UserID_1"
        },
        {
            "ResultCode": 70107,
            "ResultInfo": "Err_TLS_PT_Open_Login_Account_Not_Exist",
            "UserID": "UserID_2"
        }
    ]
}
```

### Response packet fields

| Field | Type | Description |
| ------------ | ------- | ---------------------------------------------- |
| ActionStatus | String | Request result. `OK`: successful; `FAIL`: failed |
| ErrorCode | Integer | Error code. `0`: successful; other values: failed |
| ErrorInfo | String | Error information about the request failure |
| ResultItem | Array | Array of results for different accounts |
| ResultCode | Integer | Error code for the account. `0`: successful; other values: failed |
| ResultInfo | String  | Error information about the failure to delete the account |
| UserID | String  | `UserID` of the account to delete |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), please see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30006  | An internal server error occurred while clearing relationship chain data. Try again later. |
| 30007  | Internal server timeout occurred while clearing relationship chain data. Try again later. |
| 30008  | A write conflict occurred while writing relationship chain data. You are advised to use the batch mode. |
| 40006  | An internal server error occurred while clearing profiles. Try again later.  |
| 70107  | The `UserID` to delete does not exist. Make sure that the `UserID` is valid. |
| 70169  | Server timeout. Try again later. |
| 70202  | Server timeout. Try again later. |
| 70402 | Invalid parameters. Make sure that the required fields are all entered and the parameter settings meet the protocol requirements. |
| 70403 | Request failed. App admin permissions are required to perform this operation. |
| 70500 | Internal server error. Try again later. |
| 71000 | Failed to delete accounts. Only accounts of apps using the IM Trial plan can be deleted. Your current app is using the Pro plan and therefore does not support deleting accounts. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/im_open_login_svc/account_delete) to debug this API.

## References

- Importing a Single Account ([v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953))
- Importing Multiple Accounts ([v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954))
- Querying Accounts ([v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956))
- Invalidating Account Login States ([v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957))
- Querying Account Online Status ([v4/openim/query_online_status](https://intl.cloud.tencent.com/document/product/1047/35477))
