## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API queries the downstream configuration.

Default API request rate limit: 500 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeDownStreamConfigs |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| ConfigId | No | String | Configuration ID |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| DownStreamConfigs | Array of [DownStreamConfig](/document/api/267/20474#DownStreamConfig) | Downstream configuration |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=DescribeDownStreamConfigs
&ConfigId="5674"
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "DownStreamConfigs":[
    {
        "ConfigId": "5674",
	"FromUrl": "rtmp://3737.liveplay.myqcloud.com/txlive",
	"ToUrl": "rtmp://3954.livepush2.myqcloud.com/live/3954_462724865?&txSecret=xx",
	"AreaName": "Shenzhen",
	"IspName": "China Telecom",
	"StartTime": "2018-07-06T14:40:23Z",
	"EndTime": "2018-07-06T18:05:23Z",
	"Status": "2"					
    }],
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=DescribeDownStreamConfigs)

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
| InternalError.GetBizidError | Error getting user account. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.InvalidUser | Account information error. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

