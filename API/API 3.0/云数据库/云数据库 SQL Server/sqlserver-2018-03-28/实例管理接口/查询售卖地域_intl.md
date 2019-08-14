## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeRegions) describes the Regions available.

API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeRegions |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | No | String | Common parameter; not passed in for this API |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of regions returned |
| RegionSet | Array of [RegionInfo](/document/api/238/19976#RegionInfo) | Region information array |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying All Regions

#### Input Sample Code

```
https://sqlserver.tencentcloudapi.com/?Action=DescribeRegions
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "9b0beca5-f3ea-44d3-97de-ec8f02effaea",
    "TotalCount": 9,
    "RegionSet": [
      {
        "Region": "ap-hongkong",
        "RegionName": "Hong Kong, China",
        "RegionId": 5,
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shanghai-fsi",
        "RegionName": "Shanghai Finance",
        "RegionId": 7,
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shantou",
        "RegionName": "Shantou",
        "RegionId": 2,
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "ap-tianjin",
        "RegionName": "Tianjin",
        "RegionId": 3,
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "na-toronto",
        "RegionName": "North America",
        "RegionId": 6,
        "RegionState": "UNAVAILABLE"
      },
      {
        "Region": "ap-beijing",
        "RegionName": "Beijing",
        "RegionId": 8,
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shenzhen-fsi",
        "RegionName": "Shenzhen Finance",
        "RegionId": 11,
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-guangzhou",
        "RegionName": "Guangzhou",
        "RegionId": 1,
        "RegionState": "AVAILABLE"
      },
      {
        "Region": "ap-shanghai",
        "RegionName": "Shanghai",
        "RegionId": 4,
        "RegionState": "AVAILABLE"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeRegions)

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
