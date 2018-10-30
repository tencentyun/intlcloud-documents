## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeRegions) is used to query the regions where an instance is available.

Default request rate limit: 20/sec.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeRegions |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | No | String | Common parameter. This parameter is not required for this API. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of the returned regions |
| RegionSet | Array of [RegionInfo](/document/api/238/19976#RegionInfo) | Array of regions |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query all the regions

#### Input example

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeRegions
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RegionSet": [
      {
        "Region": "ap-hongkong",
        "RegionId": 5,
        "RegionName": "Hong Kong",
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shanghai-fsi",
        "RegionId": 7,
        "RegionName": "Shanghai Finance",
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shantou",
        "RegionId": 2,
        "RegionName": "Shantou",
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "ap-tianjin",
        "RegionId": 3,
        "RegionName": "Tianjin",
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "na-toronto",
        "RegionId": 6,
        "RegionName": "North America",
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "ap-beijing",
        "RegionId": 8,
        "RegionName": "Beijing",
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shenzhen-fsi",
        "RegionId": 11,
        "RegionName": "Shenzhen Finance",
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-guangzhou",
        "RegionId": 1,
        "RegionName": "Guangzhou",
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shanghai",
        "RegionId": 4,
        "RegionName": "Shanghai",
        "RegionState": "AVAILABLE"
      }
    ],
    "RequestId": "9b0beca5-f3ea-44d3-97de-ec8f02effaea",
    "TotalCount": 9
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeRegions)

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

