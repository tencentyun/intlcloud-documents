## 1. API Description

API domain name: kms.tencentcloudapi.com

This API creates a customer master key (CMK) for data key management.

API request rate limit: 100 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/573/34406).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateKey |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-18 |
| Region | Yes | String | Common parameter. For more information, see the [List of Regions](/document/api/573/34406#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Alias | Yes | String | Alias that makes a key more recognizable and understandable. This parameter cannot be empty and can contain 1-60 characters or numbers |
| Description | No | String | CMK description of up to 1,024 bytes |
| KeyUsage | No | String | Specifies what the key is used for. Currently, only "ENCRYPT_DECRYPT" is supported. The default value is "ENCRYPT_DECRYPT", i.e., the key is used for encryption and decryption |
| Type | No | Integer | Specifies the key type. 1: default type in the current region. The default value is 1, and currently only this type is supported |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| KeyId | String | Globally unique ID of the CMK |
| Alias | String | Alias that makes a key more recognizable and understandable |
| CreateTime | Integer | Key creation time in Unix timestamp format |
| Description | String | CMK description <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| KeyState | String | CMK status |
| KeyUsage | String | CMK usage |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Creating a CMK

Create a CMK used for data key management. The CMK can be used in other APIs to create data keys, perform encryption and decryption, and do more.

#### Input Sample Code

```
https://kms.tencentcloudapi.com/?Action=CreateKey
&Alias=mykey
&KeyUsage=ENCRYPT_DECRYPT
&Description=test
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "KeyId": "9999aed0-4956-11e9-bc70-5254005e86b4",
    "Alias": "alias-0001",
    "CreateTime": 1552897190,
    "Description": "test cmk",
    "KeyState": "Enabled",
    "KeyUsage": "ENCRYPT_DECRYPT",
    "RequestId": "850bf779-2249-4995-8c55-b3966daf0a8c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool makes it easy for you to call Tencent Cloud APIs,  authenticate signature, generate SDK codes, and search for APIs. **

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=CreateKey)

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
| InvalidParameterValue.InvalidKeyUsage | Invalid KeyUsage. |
| InvalidParameterValue.InvalidType | Invalid type. |
| LimitExceeded.CmkLimitExceeded | The number of CMKs has reached the limit. |
| UnauthorizedOperation | Unauthorized operation. |
