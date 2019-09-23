## API Description

This API (ModifySubDomain) is used to modify the path mapping in the custom domain name settings of the service. The path mapping rule can be modified before it is bound to the custom domain name.

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| ---------------------------- | ---- | ------ | ---------------------------------------- |
| serviceId | Yes | String | Unique service ID. |
| subDomain | Yes | String | The custom domain name for which to modify the path mapping. |
| isDefaultMapping | Yes | String | Whether to change to the default path mapping. TRUE: use default path mapping; FALSE: use custom path mapping. |
| pathMappingSet.n.path | No | Object | Post-modification path. |
| pathMappingSet.n.environment | No | Object | Post-modification environment name. |
| protocol | No | String | Post-modification custom domain name protocol type. |
| certificateId | No | String | Certificate ID, which should be passed in when the HTTPS protocol is included. |


## Output Parameters
| Parameter Name | Type | Description |
| -------- | ------ | ---------------------------------------- |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946). |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |

## Samples 
Sample input:
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=ModifySubDomain
&serviceId=service-XXXX
&subDomain=testSubDomain
&isDefaultMapping=FALSE
&pathMapping.0.path=/test
&pathMapping.0.environment=release
```
Sample output:
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success"
}
```




