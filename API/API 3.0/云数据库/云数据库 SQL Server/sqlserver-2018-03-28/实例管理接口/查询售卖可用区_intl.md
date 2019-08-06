## 1. API Description

API domain name: sqlserver.tencentcloudapi.com.

This API (DescribeZones) describes the Availability Zones available for the product.

API request rate limit: 20 requests/sec.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/238/19930).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeZones |
| Version | Yes | String | Common parameter. The version of this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of AZs returned |
| ZoneSet | Array of [ZoneInfo](/document/api/238/19976#ZoneInfo) | AZ array |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying All AZs

#### Input Sample Code

```
https://postgres.tencentcloudapi.com/?Action=DescribeZones
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "c877d7ce-bde9-48dc-bf8c-9efb01570caa",
    "TotalCount": 34,
    "ZoneSet": [
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 1,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 5,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 17,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 16,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 14,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 6,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 2,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 14,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 3,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 14,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 4,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 26,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 20,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 13,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 5,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 23,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 3,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 4,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 6,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 5,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 1,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 4,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 13,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 6,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 21,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 25,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 24,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 13,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 19,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 3,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 2,
        "Version": "2008R2"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 22,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-2",
        "ZoneName": "Guangzhou Zone 2",
        "ZoneId": 100002,
        "SpecId": 2,
        "Version": "2012SP3"
      },
      {
        "Zone": "ap-guangzhou-3",
        "ZoneName": "Guangzhou Zone 3",
        "ZoneId": 100003,
        "SpecId": 18,
        "Version": "2012SP3"
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeZones)

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
