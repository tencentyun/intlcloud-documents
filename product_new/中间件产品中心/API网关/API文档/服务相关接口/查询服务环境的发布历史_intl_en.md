## API Description
This API (DescribeServiceEnvironmentReleaseHistory) is used to query the release history of a service environment.
A service can only be used when it is published to an environment after creation. This API is used to query the release history of an environment under a service. 

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| --------------- | ---- | ------ | ----------- |
| serviceId | Yes | String | Unique ID of the service to be queried |
| environmentName | Yes | String | Environment name |
| limit | No | Int | Number of results to be returned |
| offset | No | Int | Offset |

## Output Parameters

| Parameter Name | Type | Description |
| ----------- | ------------- | ------------------------------------------------------------ |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946) |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| totalCount | String | Total number of releases |
| versionList | List of Array | List of historical versions |

versionList is the list of historical versions, which is an array of versionAttribute. versionAttribute is composed as follows:

| Parameter Name | Type | Description |
| ----------- | ------ | ------- |
| versionName | String | Version number |
| versionDesc | String | Version description |
| releaseTime | Time | Release time |


## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=DescribeServiceEnvironmentReleaseHistory
&serviceId=service-XX
&environmentName=test
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success",
	"totalCount": 2,
	"versionList": [{
			"versionName": "version-20170904xx",
			"versionDesc": "Desc1",
			"releaseTime": "2017-06-08_21:53"
		},
		{
			"versionName": "version-20170905xx",
			"versionDesc": "Desc2",
			"releaseTime": "2017-06-08_21:54"
		}
	]
}
```




