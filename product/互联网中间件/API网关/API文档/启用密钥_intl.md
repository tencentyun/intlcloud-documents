## API Description

This API (EnableApiKey) is used to enable a pair of disabled API keys.

## Input Parameters

The following request parameter list only provides API request parameters. Other parameters can be found in [Common Request Parameters](/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | --------- |
| secretId | Yes | String | The key ID to be enabled. |

## Output Parameters
| Parameter Name | Type | Description |
| -------- | ------ | ---------------------------------------- |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946" title="Common Error Codes">Common Error Codes</a> on the Error Codes page. |
| codeDesc | String | Error code at business side. For a successful operation, "Success" is returned. In case of an error, a message describing the reason for the error is returned. |
| message | String | Module error message description depending on API. |

## Example 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=EnableApiKey
&secretId=AKIDXXXXWKipDlK
```
The returned results are as below:
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success",
}
```





