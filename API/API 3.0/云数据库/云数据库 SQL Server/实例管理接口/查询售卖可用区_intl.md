## 1. API Description

Domain name for API request: sqlserver.tencentcloudapi.com

This API (DescribeZones) is used to query availability zones.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: sqlserver.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/238/19930).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeZones |
| Version | Yes | String | Common parameter. The value used for this API: 2018-03-28 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/238/19930#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of returned availability zones |
| ZoneSet | Array of [ZoneInfo](/document/api/238/19976#ZoneInfo) | Array of returned availability zones |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query all the availability zones

#### Input example

```
https://postgres.tencentcloudapi.com/?Action=DescribeZones
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestId": "c877d7ce-bde9-48dc-bf8c-9efb01570caa",
    "TotalCount": 34,
    "ZoneSet": [
      {
        "SpecId": 1,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 5,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 17,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 16,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 14,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 6,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 2,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 14,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 3,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 14,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 4,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 26,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 20,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 13,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 5,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 23,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 3,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 4,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 6,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 5,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 1,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 4,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 13,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 6,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 21,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 25,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 24,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 13,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 19,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 3,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 2,
        "Version": "2008R2",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 22,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      },
      {
        "SpecId": 2,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-2",
        "ZoneId": 100002,
        "ZoneName": "Guangzhou Zone 2"
      },
      {
        "SpecId": 18,
        "Version": "2012SP3",
        "Zone": "ap-guangzhou-3",
        "ZoneId": 100003,
        "ZoneName": "Guangzhou Zone 3"
      }
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=sqlserver&Version=2018-03-28&Action=DescribeZones)

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
| InternalError.SystemError | System error. |
| InvalidParameter.InputIllegal | Invalid input parameter. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion failed. |
| InvalidParameterValue.IllegalRegion | Invalid region |

