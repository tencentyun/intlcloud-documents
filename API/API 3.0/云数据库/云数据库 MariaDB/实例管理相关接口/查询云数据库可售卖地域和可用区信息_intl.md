## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeSaleInfo) is used to query supported regions and availability zones of a database.

Default request rate limit: 20/sec.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeSaleInfo. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | No | String | Common parameter. This parameter is not required for this API. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RegionList | Array of [RegionInfo](/document/api/237/16191#RegionInfo) | List of information related to available regions |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query supported regions and availability zones of a database

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeSaleInfo
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RegionList": [
      {
        "AvailableChoice": [
          {
            "MasterZone": {
              "Zone": "ap-chengdu-1",
              "ZoneId": 160001,
              "ZoneName": "Chengdu Zone 1"
            },
            "SlaveZones": [
              {
                "Zone": "ap-chengdu-1",
                "ZoneId": 160001,
                "ZoneName": "Chengdu Zone 1"
              }
            ]
          }
        ],
        "Region": "ap-chengdu",
        "RegionId": 16,
        "RegionName": "Chengdu",
        "ZoneList": [
          {
            "Zone": "ap-chengdu-2",
            "ZoneId": 160002,
            "ZoneName": "Chengdu Zone 2"
          },
          {
            "Zone": "ap-chengdu-1",
            "ZoneId": 160001,
            "ZoneName": "Chengdu Zone 1"
          }
        ]
      }
    ],
    "RequestId": "e44995d7-4889-4f73-a42a-36c21120e126"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeSaleInfo)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |

