## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API queries user group list

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListGroups |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| Page | No | Integer | Page number. |
| Rp | No | Integer | Quantity per page. |
| Keyword | No | String | Filter by user group name. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalNum | Integer | Total number of user groups. |
| GroupInfo | Array of [GroupInfo](/document/api/598/33167#GroupInfo) | Array information of a user group. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying User Group List

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListGroups
&Page=20
&Rp=1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalNum": 2,
    "GroupInfo": [
      {
        "GroupId": 2021,
        "GroupName": "test2",
        "CreateTime": "2019-04-03 15:15:18",
        "Remark": "test2"
      },
      {
        "GroupId": 2020,
        "GroupName": "test1",
        "CreateTime": "2019-04-03 15:11:34",
        "Remark": "test2"
      }
    ],
    "RequestId": "dbb91d87-5e3f-42b4-8cc9-ad9f16600370"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListGroups)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).