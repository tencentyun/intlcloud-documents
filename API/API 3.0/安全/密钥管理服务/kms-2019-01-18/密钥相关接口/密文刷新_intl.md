## 1. API Description

API domain name: kms.tencentcloudapi.com

This API is used to re-encrypt a ciphertext using a specified customer master key (CMK).

API request rate limit: 100 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/573/34406).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ReEncrypt |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-18 |
| Region | Yes | String | Common parameter. For more information, see the [List of Regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/573/34406#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| CiphertextBlob | Yes | String | Ciphertext to be re-encrypted |
| DestinationKeyId | No | String | CMK used for re-encryption. If this parameter is empty, the ciphertext is re-encrypted using the original CMK (as long as the key is not rotated, the ciphertext will not be refreshed) |
| SourceEncryptionContext | No | String | Key-value pair JSON string for CiphertextBlob ciphertext encryption. This field is empty if it's not being used for encryption. |
| DestinationEncryptionContext | No | String | Key-value pair JSON string for re-encryption. To use this field, you need to fill in the same string when decrypting the returned new ciphertext. |  

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CiphertextBlob | String | Re-encrypted ciphertext |
| KeyId | String | CMK used for re-encryption |
| SourceKeyId | String | CMK used by the ciphertext before re-encryption |
| ReEncrypted | Boolean | `true` means that the ciphertext has been re-encrypted. When using the old CMK to re-encrypt,  the re-encryption will not perform until the CMK is rotated; it will return the original ciphertext. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Re-encrypting ciphertext

Re-encrypt the ciphertext.

#### Input Sample Code

```
https://kms.tencentcloudapi.com/?Action=ReEncrypt
&DestinationKeyId=23e80852-1e38-11e9-b129-5cb9019b4b01
&CiphertextBlob=Ade234dasdeEWdGVzdCUyMHBsYWlJJlIHL
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "CiphertextBlob": "g2F8eQk44QrTbfj09TL17AZyFPgs8BTtZe2j27Wuw1YzTBCxnd0T/gwFQSasmtzxZi6mmvD7DCjCE+LxJmdhXQ==-k-zJshb0kBH7C2J5I3XXbbEg==-k-o1O+7H9HFAzWbCkftO2ZtPKewS3diSB4zGKOJhMn7LcKRhYr",
    "KeyId": "23e80852-1e38-11e9-b129-5cb9019b4b01",
    "SourceKeyId": "23e80852-1e38-11e9-b129-5cb9019b0000",
    "ReEncrypted": true,
    "RequestId": "1b580852-1e38-11e9-b129-5cb9019b4b00"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool makes it easy for you to call Tencent Cloud APIs,  authenticate signature, generate SDK codes, and search for APIs. **

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=ReEncrypt)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) for various programming languages, facilitating API calls. 

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/573/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Invalid parameter. |
| InvalidParameterValue.InvalidCiphertext | Invalid ciphertext format. |
| InvalidParameterValue.InvalidKeyId | Invalid KeyId. |
| ResourceUnavailable.CmkDisabled | The CMK has been disabled. |
| ResourceUnavailable.CmkNotFound | The CMK does not exist. |
| UnauthorizedOperation | Unauthorized operation. |
