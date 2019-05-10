## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API queries the active upstream information list.

Default API request rate limit: 500 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeLiveStreamOnlineInfo |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| PageNum | Yes | Integer | The page number to get. <br/>Default value: 1. |
| PageSize | Yes | Integer | Page size. <br/>Maximum value: 100. <br/>Value range: any integer between 1 and 100. <br/>Default value: 10. |
| Status | No | Integer | 0: publishing not started; 1: publishing |
| StreamName | No | String | Stream name. |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| PageNum | Integer | Page number. |
| PageSize | Integer | Size per page |
| TotalNum | Integer | Total number of eligible ones. |
| TotalPage | Integer | Total number of pages. |
| StreamInfoList | Array of [StreamInfo](/document/api/267/20474#StreamInfo) | Stream information list |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=DescribeLiveStreamOnlineInfo
&PageNum=1
&PageSize=10
&Status=1
&<Common request parameter>
```

#### Output Sample Code

```
{
	"Response": {
		"PageNum": 1,
		"PageSize": 10,
		"RequestId": "6d7080fe-7cc5-40eb-4d44-fecdd7a33cc5",
		"StreamlInfoList": [{
			"AppName": ["live"],
			"CreateMode": "1",
			"CreateTime": "2018-07-13 14:48:23",
			"Status": 1,
			"StreamId": "10905947996257011227",
			"StreamName": "teststream",
			"WaterMarkId": "0"
		}],
		"TotalNum": 1,
		"TotalPage": 1
	}
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=DescribeLiveStreamOnlineInfo)

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
| InternalError.CallOtherSvrError | Error calling internal service. |
| InternalError.ConfigNotExist | The configuration does not exist. |
| InternalError.InvalidUser | Account information error. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |

