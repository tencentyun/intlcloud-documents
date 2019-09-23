## API Description
This API (DescribeApiKey) is used to query the details of keys.
After you have created an API secretkey, you can query its details using this API.


## Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/628/18814).

| Parameter Name | Required | Type | Description |
| -------- | ---- | ------ | -------- |
| secretID | Yes | String | API secretID |

## Output Parameters

| Parameter Name | Type | Description |
| ------------ | --------- | ---------------------------------------- |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/628/18822#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| secretName | String | User-defined secret key name. |
| secretID | String | API secretID. |
| secretKey | String | API secretKey. |
| status | Int | API key status. 1: enabled; 0: disabled. |
| type | String | API key type. auto: general; manual: custom. |
| createdTime | Timestamp | Creation time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used. |
| modifiedTime | Timestamp | Last modified time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used. |



## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=DescribeApiKey
&secretID=AKIDXXXXWKipDlK
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success",
	"secretID": "AKIDXXXXWKipDlK",
	"secretKey": "asdkXXXXKOlhKn",
	"secretName": "mytest",
	"status": 1,
	"type": "auto",
	"createdTime": "2017-08-07T00:00:00Z",
	"modifiedTime": "2017-08-07T00:00:00Z"
}
```

