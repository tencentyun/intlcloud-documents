## API Description
This API (UpdateApiKey) is used to replace a pair of created API keys.

## Input Parameters

The following request parameter list only provides API request parameters. Other parameters can be found in [Common Request Parameters](/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | --------- |
| secretId | Yes | String | The key ID to be replaced. |

## Output Parameters
| Parameter Name | Type | Description |
| ------------ | --------- | ---------------------------------------- |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946" title="Common Error Codes">Common Error Codes</a> on the Error Codes page. |
| codeDesc | String | Error code at business side. For a successful operation, "Success" is returned. In case of an error, a message describing the reason for the error is returned. |
| message | String | Module error message description depending on API. |
| secretId | String | The key ID to be replaced. |
| secretKey | String | The replaced key. |
| modifiedTime | Timestamp | Replacement time. It is in the format of YYYY-MM-DDThh:mm:ssZ according to the ISO8601 standard. UTC time is used. |

## Example 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=UpdateApiKey
&secretId=AKIDXXXXWKipDlK
```
The returned results are as below:
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success",
	"secretId":"AKIDXXXXWKipDlK",
	"secretKey":"adasfdasffa",
	"modifiedTime":"2017-08-07T00:00:00Z", 
}
```





