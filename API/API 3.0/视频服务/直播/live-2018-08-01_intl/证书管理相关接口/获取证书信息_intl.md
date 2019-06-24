## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API obtains the certificate information.

Default API request rate limit: 500 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeLiveCert |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| CertId | Yes | Integer | Certificate ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CertInfo | [CertInfo](/document/api/267/20474#CertInfo) | Certificate information |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Getting Certificate Details

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=DescribeLiveCert
&CertId=1000
&<Common request parameter>
```

#### Output Sample Code

```
{
       "Response": {
	    "CertInfo": {
		"CertId": 1000,
		"CertName": "testName",
		"Description": "testDesc",
		"CreateTime": "2018-11-30T15:50:12Z",
		"HttpsCrt": "xxx",
		"CertType": 0,
		"CertExpireTime": "2018-12-30T15:50:12Z",
		"DomainList": ["5000.livepush.play.com"]
	    },
	    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
	}
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=DescribeLiveCert)

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
| FailedOperation.InvokeVideoApiFail | An exception occurred when operation the VOD API. |
| InternalError | Internal error |
| InternalError.CrtDomainNotFound | There is no related domain name. |
| InternalError.DBError | DB execution error. |
| InternalError.InvalidInput | Parameter check failed. |

