## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (DescribeProcesses) is used to obtain the process list.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeProcesses |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| Uuid | No | String | Unique Uuid of the HS client. Either Uuid or ProcessName should be specified. If Uuid is specified, it means querying the host list. |
| ProcessName | No | String | Process name. Either Uuid or ProcessName should be specified. If ProcessName is specified, it means querying the list of the specified process. |
| Limit | No | Integer | Number of returned results. It defaults to 10. The maximum is 100. |
| Offset | No | Integer | Offset. It defaults to 0. |
| Filters.N | No | Array of [Filter](/document/api/296/19867#Filter) | Filter condition. <br/><li>ProcessName - String - Required: No - Process name</li><li>MachineIp - String - Required: No - Host private IP</li> |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of records in the process list. |
| Processes | Array of [Process](/document/api/296/19867#Process) | Array of the process list |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Obtain the process list

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=DescribeProcesses
&Limit=10
&Offset=0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "TotalCount": 100,
    "Processes": [
      {
        "Username": "root",
        "Uuid": "6b6cd843-6bc1-4011-a74c-dc3fd26a7dd1",
        "Platform": "LINUX32",
        "MachineName": "machine-name",
        "Pid": 14456,
        "Id": 1,
        "ProcessName": "mysql",
        "CreateTime": "2018-01-01 12:12:12",
        "FullPath": "/usr/local/mysql/bin/mysql",
        "Ppid": 13456,
        "MachineIp": "10.12.13.22"
      }
    ],
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=DescribeProcesses)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/296/19830#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.IllegalRequest | Invalid request. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |
| InvalidParameter.ParsingError | Parameter parsing error. |
| MissingParameter | A parameter is missing. |

