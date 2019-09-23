## API Description

This API (DescribeServiceReleaseVersion) is used to query the list of all released versions under a service.
A service is generally released with several versions. This API can be used to query the released versions.

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ----------- |
| serviceId | Yes | String | Unique ID of the service to be queried |
| limit | No | Int | Number of results to be returned |
| offset | No | Int | Offset |


## Output Parameters
| Parameter Name | Type | Description |
| ----------- | ------------- | ------------------------------------------------------------ |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946) |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| totalCount | String | Total number of releases |
| versionList | List of Array | Version list |

versionList is the list of historical versions, which is an array of versionAttribute. versionAttribute is composed as follows:

| Parameter Name | Type | Description |
| ------------ | -------------- | ------------- |
| versionName | String | Version number |
| versionDesc | String | Version description |
| environments | List of String | List of currently released environments for this version |
| createTime | Time | Version creation time |

## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=DescribeServiceReleaseVersion
&serviceId=service-XX
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
			"versionDesc": "desc",
			"environments": [
				"test",
				"prepub"
			],
			"createTime": "2017-09-27 00:00::00"
		},
		{
			"versionName": "version-20170905xx",
			"versionDesc": "desc",
			"environments": [
				"release"
			],
			"createTime": "2017-09-27 00:00::00"
		}
	]
}
```




