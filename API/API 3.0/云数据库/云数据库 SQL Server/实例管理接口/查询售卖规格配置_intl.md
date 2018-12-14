## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeProductConfig) is used to query the available specifications.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeProductConfig |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability zone ID, such as ap-guangzhou-1 |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| SpecInfoList | Array of [SpecInfo](/document/api/238/19976#SpecInfo) | Array of specifications |
| TotalCount | Integer | Total number of returned data entries |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the available specifications in an availability zone in a region

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeProductConfig
&Zone=ap-guangzhou-2
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestId": "f4f78ba3-9ce1-42e0-bc42-470460cbdd11",
    "SpecInfoList": [
      {
        "CPU": 2,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 300,
        "Memory": 4,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 4000,
        "SpecId": 2,
        "SuitInfo": "Small projects with hundreds of independent users",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 2,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 300,
        "Memory": 4,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 4000,
        "SpecId": 2,
        "SuitInfo": "Small projects with hundreds of independent users",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 1,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 300,
        "Memory": 2,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 2100,
        "SpecId": 1,
        "SuitInfo": "Small projects with hundreds of independent users",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 8,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 16,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 16800,
        "SpecId": 4,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 6,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 12,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 12750,
        "SpecId": 13,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 12,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 24,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 20000,
        "SpecId": 14,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 4,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 8,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 6500,
        "SpecId": 3,
        "SuitInfo": "Small projects with thousands of independent users",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 8,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 16,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 16800,
        "SpecId": 4,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 12,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 24,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 20000,
        "SpecId": 14,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 6,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 12,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 12750,
        "SpecId": 13,
        "SuitInfo": "Small projects with independent users at 10k level",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 4,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 500,
        "Memory": 8,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 6500,
        "SpecId": 3,
        "SuitInfo": "Small projects with thousands of independent users",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 22,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 1000,
        "Memory": 48,
        "MinStorage": 1000,
        "Pid": 10908,
        "QPS": 36300,
        "SpecId": 6,
        "SuitInfo": "Medium projects with independent users at 1,000k level",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      },
      {
        "CPU": 22,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 1000,
        "Memory": 48,
        "MinStorage": 1000,
        "Pid": 10908,
        "QPS": 36300,
        "SpecId": 6,
        "SuitInfo": "Medium projects with independent users at 1,000k level",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 16,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 1000,
        "Memory": 32,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 23000,
        "SpecId": 5,
        "SuitInfo": "Medium projects with independent users at 100k level",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012"
      },
      {
        "CPU": 16,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "MaxStorage": 1000,
        "Memory": 32,
        "MinStorage": 10,
        "Pid": 10908,
        "QPS": 23000,
        "SpecId": 5,
        "SuitInfo": "Medium projects with independent users at 100k level",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2"
      }
    ],
    "TotalCount": 15
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeProductConfig)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/238/19932#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DBError | Database error |
| InternalError.SystemError | System error |
| InvalidParameter.InputIllegal | Invalid input parameter |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed |
| InvalidParameterValue.IllegalRegion | Invalid region |
| InvalidParameterValue.IllegalZone | Invalid availability zone ID |

