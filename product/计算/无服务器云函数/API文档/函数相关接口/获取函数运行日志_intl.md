## 1. API Description
API request domain name: scf.tencentcloudapi.com.
This API returns the function logs according to the configured log query criteria.
Default API request frequency limit: 20 times/second.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/583/17238).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: GetFunctionLogs |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | No | String | Name of the function |
Offset | No | Integer | Offset of the data; Offset+Limit cannot be greater than 10000 |
| Limit | No | Integer | Length of the returned data; Offset+Limit cannot be greater than 10000 |
| Order | No | String | This indicates whether the logs are sorted in ascending or descending order; possible values: desc and acs |
| OrderBy | No | String | This is to sort logs by a specific field; the following fields are supported: startTime, functionName, requestId, duration and memUsage |
| Filter | No | [Filter](/document/api/583/17244#Filter) | | Log filtering condition. This can be used to distinguish between logs for successes and logs for errors. filter.retCode=not0 indicates that only the logs for errors are returned, while filter.retCode=is0 indicates that only the logs for successes are returned; if this parameter is blank, all logs are returned |
| Qualifier | No | String | Version of the function |
| FunctionRequestId | No | String | The requestId that executes this function |
| StartTime | No | Timestamp | The specific start time of the query, for example, 2017-05-16 20:00:00. It can be only less than one day before the endTime |
| EndTime | No | Timestamp | The specific end time of the query, for example, 2017-05-16 20:59:59. It can be only less than one day after the startTime |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of function logs |
| Data | Array of [FunctionLog](/document/api/583/17244#FunctionLog) | Function log information |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |
## 4. Sample
### Getting Function Logs
#### Input Sample Code
```
https://scf.tencentcloudapi.com/?Action=GetFunctionLogs
&FunctionName=<FunctionName>
&<Common request parameter>
```
#### Output Sample Code
```
{
    "Response": {
        "TotalCount": 1,
        "Data": [
            {
                "MemUsage": 3174400,
                "RetCode": 1,
                "RetMsg": "Success",
                "Log": "",
                "BillDuration": 100,
                "InvokeFinished": 1,
                "RequestId": "bc309eaa-6d64-11e8-a7fe-5254000b4175",
                "StartTime": "2018-06-11 18:46:45",
                "Duration": 0.532,
                "FunctionName": "APITest"
            }
        ],
        "RequestId": "e2571ff3-da04-4c53-8438-f58bf057ce4a"
    }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=GetFunctionLogs)
### SDK
Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.
* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
### TCCLI
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)
## 6. Error Codes
Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/583/17240#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.System | Internal system error. |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.DateTime | Wrong DateTime parameter passed in. |
| LimitExceeded.Offset | Offset is out of range. |
| UnauthorizedOperation.CAM | CAM authentication failed. |

