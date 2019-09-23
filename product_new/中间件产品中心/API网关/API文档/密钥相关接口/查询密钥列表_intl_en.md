## API Description
This API (DescribeApiKeysStatus) is used to query the list of keys.
If you have created multiple API key pairs, you can use this API to query the information of one or more keys. This API does not display the secretKey.


## Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/628/18814).

| Parameter Name | Required | Type | Description |
| ----------- | ---- | ---------------- | ---------------------------------------- |
| secretIDs.n | No | Array of Strings | Queries by one or more API secretIDs. If no secretID is entered, the information of the first 20 keys will be returned by default. |
| offset | No | Int | Offset. Default value: 0. |
| limit | No | Int | Number of results to be returned. Default value: 20. Maximum value: 100. |
| orderby | No | String | Sort by field. |
| order | no | String | Sorting order. |
| searchName | No | String | Fuzzy search by key name. |
| searchId | No | String | Exact search by unique key ID. |

## Output Parameters

| Parameter Name | Type | Description |
| --------------- | ------------- | ---------------------------------------- |
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/628/18822#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| message | String | API-related module error message description. |
| totalCount | Int | Number of eligible API keys. |
| apiKeyStatusSet | List of Array | API key list. |

Here, apiKeyStatusSet is an array of apiKeyStatus. apiKeyStatus is composed as follows:

| Parameter Name | Type | Description |
| ------------ | --------- | ---------------------------------------- |
| secretID | String | API secretID. |
| secretName | String | User-defined secret key name. |
| status | Bollen | Key status. There are currently two values: 1 (enabled) and 0 (disabled). |
| type | String | Key type. There are currently two values: auto (general type) and manual (custom type). |
| createdTime | Timestamp | Creation time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used. |
| modifiedTime | Timestamp | Last modified time in the format of YYYY-MM-DDThh:mm:ssZ according to ISO8601 standard. UTC time is used. |

## Samples 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<Common Request Parameter>
&Action=DescribeApiKeysStatus
&secretIDs.0=AKIDXXXXWKipDlK
&secretIDs.1=AKIDXXXXAVd3EuW
&offet=0
&limit=2
&orderby=createdTime
&order=desc
&searchKey=aa
```
Below is a sample return:
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success",
	"totalCount": 2,
	"apiKeyStatusSet": [{
			"secretID": "AKIDXXXXWKipDlK",
			"secretName": "myTest",
			"status": 1,
			"createdTime": "2017-08-07T00:00:00Z",
			"modifiedTime": "2017-08-07T00:00:00Z",
			"type": "auto"
		},
		{
			"secretID": "AKIDXXXXAVd3EuW",
			"secretName": "myTest1",
			"status": 0,
			"createdTime": "2017-08-07T00:10:00Z",
			"modifiedTime": "2017-08-07T00:10:00Z",
			"type": "auto"
		}
	]
}
```




