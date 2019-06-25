## 1. API Description

API request domain name: scf.tencentcloudapi.com.

This API returns the filtered function logs based on the query criteria.

Default API request frequency limit: 20 times/second.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/583/17238).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: GetFunctionLogs |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | No | String | Name of the function |
| Offset | No | Integer | Offset of the data; Offset+Limit cannot be greater than 10000 |
| Limit | No | Integer | Length of the returned data; Offset+Limit cannot be greater than 10000 |
| Order | No | String | Sorting query results in either ascending or descending order; valid values: desc, acs |
| OrderBy | No | String | Sorting the query result in either ascending or descending according to one or more fields, including startTime, functionName, requestId, duration and memUsage |
| Filter | No | [Filter](/document/api/583/17244#Filter) | | Log filters. filter.retCode=not0 indicates that only the logs of failed requests are returned; filter.retCode=is0 indicates that only the logs for successful requests are returned; if this parameter is blank, all logs are returned. |
| Qualifier | No | String | Version of the function |
| FunctionRequestId | No | String | The requestId that executes this function |
| StartTime | No | Timestamp | The specific start time of the query, for example, 2017-05-16 20:00:00. The maximum difference between StartTime and EndTime is 24 hours.|
| EndTime | No | Timestamp | The specific end time of the query, for example, 2017-05-16 20:59:59. The maximum difference between StartTime and EndTime is 24 hours. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of function logs |
| Data | Array of [FunctionLog](/document/api/583/17244#FunctionLog) | Function log information |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=GetFunctionLogs)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/583/17240#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.System | Internal system error. |
| InvalidParameterValue | An invalid value was declared for the input parameter. |
| InvalidParameterValue.DateTime | An invalid value was declared for the input parameter: DateTime |
| LimitExceeded.Offset | Offset is out of range. |
| UnauthorizedOperation.CAM | CAM authentication failed. |

