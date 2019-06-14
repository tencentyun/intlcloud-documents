## 1. API Description

API domain name: cam.tencentcloudapi.com.

Query SAML identity provider details

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: GetSAMLProvider |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| Name | Yes | String | SAML identity provider name |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Name | String | Name of the SAML identity provider |
| Description | String | Description of the SAML identity provider |
| CreateTime | Timestamp | Creation time of the SAML identity provider |
| ModifyTime | Timestamp | Last modified time of the SAML identity provider |
| SAMLMetadata | String | Metadata document of the SAML identity provider |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying SAML Identity Provider Details

Query identity provider details

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=GetSAMLProvider
&Name=okta
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Name": "okta",
    "Description": "okta",
    "CreateTime": "2018-09-17 17:18:03",
    "ModifyTime": "2018-09-17 17:18:03",
    "SAMLMetadata": "U0FNTE1ldGFkYXRh"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=GetSAMLProvider)

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
| ResourceNotFound.IdentityNotExist | The identity provider does not exist. |
| ResourceNotFound.NotFound | The resource does not exist. |