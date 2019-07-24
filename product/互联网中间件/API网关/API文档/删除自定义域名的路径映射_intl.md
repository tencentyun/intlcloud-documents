## API Description

This API (DeleteServiceSubDomainMapping) is used to delete a custom domain name mapping of an environment in the service.
If a user uses a custom domain name and a custom mapping, this API can be used. Please note that if the mappings of all environments are deleted, calling this API will return a failure.


## Input Parameters

The following request parameter list only provides API request parameters. Other parameters can be found in [Common Request Parameters](/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ------ | ----------- |
| serviceId | Yes | String | The unique ID of the service. |
| subDomain | Yes | String | The custom domain name bound to the service. |
| environment | Yes | String | The name of the environment where the mapping is to be deleted. |

## Output Parameters
| Parameter Name | Type | Description |
| -------- | ------ | ---------------------------------------- |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946" title="Common Error Codes">Common Error Codes</a> on the Error Codes page. |
| codeDesc | String | Error code at business side. For a successful operation, "Success" is returned. In case of an error, a message describing the reason for the error is returned. |


## Example 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=DeleteServiceSubDomainMapping
&serviceId=service-XXXX
&subDomain=www.qq.com
&environment=test
```
The returned results are as below:
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success",
}
```





