## API Description

This API (DescribeService) is used to query the details of a service, such as its description, domain name, protocol, creation time, and releases.

## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ----------- |
| serviceId | Yes | String | Unique ID of the service to be queried |

## Output Parameters

| Parameter Name | Type | Description |
| --------------------- | -------------- | ------------------------------------------------------------ |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81" title="Common Error Codes">Common Error Codes</a> on the Error Codes page |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| serviceId | String | Unique service ID |
| serviceName | String | User-defined service name |
| serviceDesc | String | Service description |
| subDomain | String | The domain name automatically assigned to the service by the system |
| protocol | String | Frontend request type of the service, such as HTTP and HTTPS |
| createdTime | Timestamp | Creation time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used |
| modifiedTime | Timestamp | Last modified time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used |
| availableEnvironments | List Of String | List of released environments, such as Test, Pre, and release |

## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=DescribeService
&serviceId=service-XX
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success",
	"serviceId": "service-XX",
	"serviceName": "test1",
	"serviceDesc": "test1",
	"subDomain": "523e8dc7bbe04613b5b1d726c2a7889d-apigateway.ap-guangzhou.qcloud.com",
	"protocol": "http",
	"createdTime": "2017-08-07T00:00:00Z",
	"modifiedTime": "2017-08-07T00:00:00Z",
	"availableEnvironments": [
		"Pre",
		"release"
	]
}
```

