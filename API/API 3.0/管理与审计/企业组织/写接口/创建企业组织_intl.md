## 1. API Description

API request domain name: organization.tencentcloudapi.com.

This API is used to create a Tencent Cloud Organization.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/850/38722).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: CreateOrganization |
| Version | Yes | String | Common parameter; the version of this API: 2018-12-25 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| OrgType | Yes | Integer | Organization type (currently fixed as 1) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| OrgId | Integer | Tencent Cloud Organization ID |
| Nickname | String | The alias of the creator |
| Mail | String | The email of the creator |
| OrgType | Integer | Organization type |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId must be provided when troubleshooting issues. |

## 4. Example

### Example 1: Creating a Tencent Cloud Organization

#### Input Example

```
https://organization.tencentcloudapi.com/?Action=CreateOrganization
&OrgType=1
&<Common request parameters>
```

#### Output Example

```
{
  "Response": {
    "OrgId": 123,
    "Nickname": "test",
    "Mail": "test@qq.com",
    "OrgType": 1,
    "RequestId": "b46d2afe-6893-4529-bc96-2c82d9214957"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=organization&Version=2018-12-25&Action=CreateOrganization)

### SDK

TencentCloud API 3.0 integrates SDKs that support various programming languages to make it easier for you to call APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/850/38725#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.OrganizationExistAlready | The Tencent Cloud Organization already exists. |
| ResourceNotFound.UserNotExist | The user does not exist. |
