﻿## 1. API Description

API domain name: cam.tencentcloudapi.com.

This SPI lists the user groups associated with a user.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](https://cloud.tencent.com/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListGroupsForUser |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| Uid | Yes | Integer | Sub-user UID |
| Rp | No | Integer | Quantity per page. |
| Page | No | Integer | Page number. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalNum | Integer | Total number of user groups to which the sub-user is added |
| GroupInfo | Array of [GroupInfo](https://cloud.tencent.com/document/api/598/33167#GroupInfo) | User group information |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Listing the User Groups Associated with a User

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListGroupsForUser
&Uid=1001408
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalNum": 1,
    "GroupInfo": [
      {
        "GroupId": 2020,
        "GroupName": "test1",
        "CreateTime": "2019-04-03 15:11:34",
        "Remark": "test2"
      }
    ],
    "RequestId": "a614c392-3079-4dab-b819-0ab0563a32f0"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListGroupsForUser)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| ResourceNotFound.UserNotExist | The user does not exist. |