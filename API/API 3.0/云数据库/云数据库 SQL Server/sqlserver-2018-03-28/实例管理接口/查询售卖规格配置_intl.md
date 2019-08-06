## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeProductConfig) describes the sale specification configuration.

API request rate limit: 20 requests/sec.




## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeProductConfig |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | AZ ID in the format of ap-guangzhou-1 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| SpecInfoList | Array of [SpecInfo](/document/api/238/19976#SpecInfo) | Specification information array |
| TotalCount | Integer | Number of date entries returned |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the Sale Specification Information in an AZ in a Region

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeProductConfig
&Zone=ap-guangzhou-2
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "f4f78ba3-9ce1-42e0-bc42-470460cbdd11",
    "TotalCount": 15,
    "SpecInfoList": [
      {
        "SpecId": 2,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 4,
        "CPU": 2,
        "MinStorage": 10,
        "MaxStorage": 300,
        "QPS": 4000,
        "SuitInfo": "Small applications with hundreds of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 2,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 4,
        "CPU": 2,
        "MinStorage": 10,
        "MaxStorage": 300,
        "QPS": 4000,
        "SuitInfo": "Small applications with hundreds of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 1,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 2,
        "CPU": 1,
        "MinStorage": 10,
        "MaxStorage": 300,
        "QPS": 2100,
        "SuitInfo": "Small applications with hundreds of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 4,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 16,
        "CPU": 8,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 16800,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 13,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 12,
        "CPU": 6,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 12750,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 14,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 24,
        "CPU": 12,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 20000,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 3,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 8,
        "CPU": 4,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 6500,
        "SuitInfo": "Small applications with thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 4,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 16,
        "CPU": 8,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 16800,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 14,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 24,
        "CPU": 12,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 20000,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 13,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 12,
        "CPU": 6,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 12750,
        "SuitInfo": "Small applications with tens of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 3,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 8,
        "CPU": 4,
        "MinStorage": 10,
        "MaxStorage": 500,
        "QPS": 6500,
        "SuitInfo": "Small applications with thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 6,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 48,
        "CPU": 22,
        "MinStorage": 1000,
        "MaxStorage": 1000,
        "QPS": 36300,
        "SuitInfo": "Medium-sized applications with millions of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 6,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 48,
        "CPU": 22,
        "MinStorage": 1000,
        "MaxStorage": 1000,
        "QPS": 36300,
        "SuitInfo": "Medium-sized applications with millions of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 5,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2012SP3",
        "VersionName": "SQL Server 2012",
        "Memory": 32,
        "CPU": 16,
        "MinStorage": 10,
        "MaxStorage": 1000,
        "QPS": 23000,
        "SuitInfo": "Medium-sized applications of hundreds of thousands of unique users",
        "Pid": 10908
      },
      {
        "SpecId": 5,
        "MachineType": "Z3",
        "MachineTypeName": "High IO",
        "Version": "2008R2",
        "VersionName": "SQL Server 2008 R2",
        "Memory": 32,
        "CPU": 16,
        "MinStorage": 10,
        "MaxStorage": 1000,
        "QPS": 23000,
        "SuitInfo": "Medium-sized applications of hundreds of thousands of unique users",
        "Pid": 10908
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeProductConfig)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/238/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.DBError | Database error. |
| InternalError.SystemError | System error. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.IllegalRegion | Invalid region. |
| InvalidParameterValue.IllegalZone | Invalid AZ ID. |
