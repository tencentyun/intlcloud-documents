## 1. API Description

API domain name: kms.tencentcloudapi.com

This API modifies the alias for the specified customer master key (CMK).

API request rate limit: 100 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/573/34406).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: UpdateAlias |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-18 |
| Region | Yes | String | Common parameter. For more information, see the [List of Regions](/document/api/573/34406#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Alias | Yes | String | New alias containing 1-64 characters or numbers |
| KeyId | Yes | String | Globally unique ID of the CMK |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Modifying an Alias

Modify the alias of the specified CMK.

#### Input Sample Code

```
https://kms.tencentcloudapi.com/?Action=UpdateAlias
&KeyId=23e80852-1e38-11e9-b129-5cb9019b4b01
&Alias=NewAlias
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1b580852-1e38-11e9-b129-5cb9019b4b00"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool makes it easy for you to call Tencent Cloud APIs,  authenticate signature, generate SDK codes, and search for APIs. **

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=UpdateAlias)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) for various programming languages, facilitating API calls. 

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/573/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue.AliasAlreadyExists | The alias already exists. |
| InvalidParameterValue.InvalidAlias | The alias is in incorrect format. |
| InvalidParameterValue.InvalidKeyId | Invalid KeyId. |
| ResourceUnavailable.CmkNotFound | The CMK does not exist. |
| UnauthorizedOperation | Unauthorized operation. |
