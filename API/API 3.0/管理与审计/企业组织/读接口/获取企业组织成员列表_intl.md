## 1. API Description

API request domain name: organization.tencentcloudapi.com.

This API is used to obtain the Tencent Cloud Organization member list.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/850/38722).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value used for this API: ListOrganizationMembers |
| Version | Yes | String | Common parameter; the version of this API: 2018-12-25 |
| Region | No | String | Common parameter; this parameter is not required for this API. |
| Offset | No | Integer | Offset |
| Limit | No | Integer | Limit number |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Members | Array of [OrgMember](https://cloud.tencent.com/document/api/850/38749#OrgMember) | Member list |
| TotalCount | Integer | Total number |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId must be provided when troubleshooting issues. |

## 4. Example

### Example 1: Obtaining the TCO Member List

#### Input Example

```
https://organization.tencentcloudapi.com/?Action=ListOrganizationMembers
&Offset=0
&Limit=10
&<Common request parameters>
```

#### Output Example

```
{
  "Response": {
    "TotalCount": 0,
    "Members": [
      {
        "Uin": 1,
        "Name": "aa",
        "Remark": "",
        "JoinTime": "2019-10-10 00:00:00"
      }
    ],
    "RequestId": "789d9d58-8e51-4b50-b3d7-f851216c5e9c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=organization&Version=2018-12-25&Action=ListOrganizationMembers)

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
| ResourceNotFound.OrganizationNotExist | The Tencent Cloud Organization does not exist. |
