## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API (ListEntitiesForPolicy) queries the list of entities associated with a policy.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListEntitiesForPolicy |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| PolicyId | Yes | Integer | Policy ID |
| Page | No | Integer | Page number starting from 1; 1 by default |
| Rp | No | Integer | Number of entries per page; 20 by default |
| EntityFilter | No | String | Valid values: All, User, Group, and Role. "All" means all entity types will be returned; "User" means only sub-accounts will be returned; "Group" means only user groups will be returned; and "Role" means only roles will be returned. "All" is the default value. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalNum | Integer | Total number of entities <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| List | Array of [AttachEntityOfPolicy](/document/api/598/33167#AttachEntityOfPolicy) | Entity list <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying the List of Entities Associated with a Policy

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListEntitiesForPolicy
&PolicyId=524497
&Page=1
&Rp=10
&EntityFilter=All
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "List": [
      {
        "Id": "1133398",
        "RelatedType": 1,
        "Uin": 3449203261,
        "Name": "test1"
      }
    ],
    "TotalNum": 10,
    "RequestId": "836d7034-9854-44f0-9d4a-ee57842f8644"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListEntitiesForPolicy)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.SystemError | Internal error. |
| InvalidParameter.EntityFilterError | The EntityFilter field is invalid. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.PolicyIdError | The input parameter PolicyId is invalid. |
