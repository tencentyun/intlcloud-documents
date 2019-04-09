## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API adds a certificate.

Default API request frequency limit: 200 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateLiveCert |
| Version | Yes | String | Common parameter; the value for this API: 2018-08-01 |
| Region | No | String | Common parameter; not passed in for this API |
| CertType | Yes | Integer | Certificate type. 0 - user-added certificate; 1 - Tencent Cloud-hosted certificate |
| HttpsCrt | Yes | String | Certificate content, i.e., the public key |
| HttpsKey | Yes | String | Private key |
| CertName | No | String | Certificate name |
| Description | No | String | Description |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CertId | Integer | Certificate ID |
| RequestId | String | The unique request ID which is returned for each request The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Adding a Certificate

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateLiveCert
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

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateLiveCert)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.CrtDateNotLegal | The certificate is invalid. |
| InternalError.CrtDateOverdue | The certificate has expired. |
| InternalError.CrtKeyNotMatch | The certificate key does not match. |
| InternalError.DBError | DB execution error. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.SystemError | Internal system error. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

