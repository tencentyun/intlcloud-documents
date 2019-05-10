## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API modifies the certificate.

Default API request rate limit: 200 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyLiveCert |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| CertId | Yes | String | Certificate ID. |
| CertType | No | Integer | Certificate type. 0 - user-added certificate; 1 - Tencent Cloud-hosted certificate |
| CertName | No | String | Certificate name |
| HttpsCrt | No | String | Certificate content, i.e., the public key |
| HttpsKey | No | String | Private key |
| Description | No | String | Description information |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Modifying a Certificate

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=ModifyLiveCert
&CertId=1000
&CertType=1
&CertName=name-crt
&HttpsCrt=XXXXX
&HttpsKey=YYYYYY
&Description=detail
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
    }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=ModifyLiveCert)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.CrtDateInUsing | The certificate is in use. |
| InternalError.CrtDateOverdue | The certificate has expired. |
| InternalError.CrtKeyNotMatch | The certificate key does not match. |
| InternalError.DBError | DB execution error. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.SystemError | Internal system error. |

