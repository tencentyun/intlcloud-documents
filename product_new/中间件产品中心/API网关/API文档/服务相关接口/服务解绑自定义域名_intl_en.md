## API Description

This API (UnBindSubDomain) is used to unbind a custom domain name.
After you have bound a custom domain name to a service using API Gateway, this API can be used if you want to unbind it.

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ----------- |
| serviceId | Yes | String | Unique service ID |
| subDomain | Yes | String | Custom domain name to be unbound |

## Output Parameters
| Parameter Name | Type | Description |
| -------- | ------ | ------------------------------------------------------------ |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946) |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |


## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=UnBindSubDomain
&serviceId=service-XXXX
&subDomain=testSubDomain
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success"
}
```
