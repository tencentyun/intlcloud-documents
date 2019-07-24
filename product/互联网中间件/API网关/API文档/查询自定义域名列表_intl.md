## API Description

This API (DescribeServiceSubDomains) is used to query the custom list.
A custom domain name can be bound to a service for calling using the API gateway. This API is used to query the list of custom domain names bound to a service.


## Input Parameters

The following request parameter list only provides API request parameters. Other parameters can be found in [Common Request Parameters](/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| --------- | ---- | ------ | ------- |
| serviceId | Yes | String | The unique ID of the service. |

## Output Parameters

| Parameter Name | Type | Description |
| ---------- | ------------- | ---------------------------------------- |
| code | Int | Common error code. 0: Successful; other values: Failed. For more information, see <a href="https://intl.cloud.tencent.com/document/product/377/8946" title="Common Error Codes">Common Error Codes</a> on the Error Codes page. |
| codeDesc | String | Error code at business side. For a successful operation, "Success" is returned. In case of an error, a message describing the reason for the error is returned. |
| totalCount | Int | The number of custom domain names under a service. |
| domainSet | List of Array | The list of domain names. |

domainSet is a list of domain names. It consists of domainStatus which is composed as follows:

| Parameter Name | Type | Description |
| ------------- | ------ | ------------------------------ |
| domainName | String | Domain name. |
| status | String | Status of domain name resolution. True: Resolution successful; False: Resolution failed. |
| certificateId | String | Certificate ID. |


## Example 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common request parameters>
&Action=DescribeSubDomain
&serviceId=service-XXXX
```
The returned results are as below:
```
{
    "code":"0",
    "message":"",
    "codeDesc":"Success",
	"totalCount":2,
	"domainSet":[
		{
			"domainName":"domain1",
			"status":"True",
			"certificateId":XXXX,
		},
		{
			"domainName":"domain2",
			"status":"Flase",
			"certificateId":XXXX,
		}
	]
}
```





