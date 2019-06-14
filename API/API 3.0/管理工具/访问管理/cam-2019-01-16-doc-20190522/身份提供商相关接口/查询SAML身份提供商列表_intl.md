## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API queries SAML identity provider list.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListSAMLProviders |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of SAML identity providers |
| SAMLProviderSet | Array of [SAMLProviderInfo](/document/api/598/33167#SAMLProviderInfo) | SAML identity provider list |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying SAML Identity Provider List

Query identity provider list

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListSAMLProviders
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 6,
    "SAMLProviderSet": [
      {
        "Name": "saml-sdk",
        "Description": "sdk",
        "CreateTime": "2018-12-17 16:33:35",
        "ModifyTime": "2019-02-26 13:34:58"
      },
      {
        "Name": "TestSAML",
        "Description": "111",
        "CreateTime": "2018-11-08 19:27:27",
        "ModifyTime": "2019-04-30 11:23:12"
      },
      {
        "Name": "OneLogin",
        "Description": "ONeLogin",
        "CreateTime": "2018-11-04 20:36:41",
        "ModifyTime": "2018-11-23 23:56:09"
      },
      {
        "Name": "Azure_AD",
        "Description": "Azure AD",
        "CreateTime": "2018-11-04 16:44:25",
        "ModifyTime": "2019-02-14 10:38:27"
      },
      {
        "Name": "api-test",
        "Description": "API test",
        "CreateTime": "2018-10-30 11:40:19",
        "ModifyTime": "2018-10-30 11:40:19"
      },
      {
        "Name": "okta",
        "Description": "okta",
        "CreateTime": "2018-09-17 17:18:03",
        "ModifyTime": "2018-09-17 17:18:03"
      }
    ],
    "RequestId": "d644fa50-7e54-4448-84d8-64cb4dd9f737"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListSAMLProviders)

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