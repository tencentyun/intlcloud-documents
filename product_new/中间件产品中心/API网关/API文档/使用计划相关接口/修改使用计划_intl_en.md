## API Description

This API (ModifyUsagePlan) is used to modify the name, description, and QPS of a usage plan.

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| ------------------- | ---- | ------ | ----------------- |
| UsagePlanId | Yes | String | Unique usage plan ID |
| usagePlanName | No | String | Modified user-defined usage plan name |
| usagePlanDesc | No | String | Modified user-defined usage plan description |
| maxRequestNumPreSec | No | Int | Limit of requests per second |
| maxRequestNum | No | Int | Total number of requests allowed. -1 indicates it’s disabled |

## Output Parameters

| Parameter Name | Type | Description |
| ------------------- | --------- | ------------------------------------------------------------ |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946) |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| UsagePlanId | String | Unique usage plan ID |
| usagePlanName | String | Modified user-defined usage plan name |
| usagePlanDesc | String | Modified user-defined usage plan description  |
| maxRequestNumPreSec | Int | Modified request per second limit |
| modifiedTime | Timestamp | Last modified time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used |

## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=ModifyUsagePlan
&usagePlanId=usagePlan-XX
&usagePlanName=newusagePlanName
&usagePlanDesc=newUsagePlanDescription
&maxRequestNumPreSec=1000
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success",
	"usagePlanId": "usagePlan-XX",
	"usagePlanName": "newusagePlanName",
	"usagePlanDesc": "newUsagePlanDescription",
	"maxRequestNumPreSec": 1000,
	"modifiedTime": "2017-08-07T00:00:00Z"
}
```




