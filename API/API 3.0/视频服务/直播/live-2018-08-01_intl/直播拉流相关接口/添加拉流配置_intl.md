## 1. API Description

API request domain name: live.tencentcloudapi.com.

This API adds downstream configuration; currently, up to 10 tasks can be added.

Default API request rate limit: 100 requests/second.

## 2. Request Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateDownStreamConfig |
| Version | Yes | String | Common parameter; the version of this API: 2018-08-01 |
| Region | No | String | Common parameter; optional for this API |
| FromUrl | Yes | String | Source URL |
| ToUrl | Yes | String | Target URL. Currently, this target address can only be a Tencent domain name. |
| AreaId | Yes | Integer | Region ID; 1 - Shenzhen, 2 - Shanghai, 3 - Tianjin, 4 - Hong Kong. |
| IspId | Yes | Integer | ISP ID; 1 - China Telecom, 2 - China Mobile, 3 - China Unicom, 4 - other; if the AreaId is 4, the IspId can only be other. |
| StartTime | Yes | String | Start time. <br/>In UTC format. <br/>For example: 2019-01-08T10:00:00Z. |
| EndTime | Yes | String | End time. Note: <br/>1. The end time must be older than the start time; <br/> 2. The end time and start time must be older than the current time; <br/>3. The difference between the end time and the start time must be less than seven days. <br/>In UTC format. <br/>For example: 2019-01-08T10:00:00Z. |

## 3. Return Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ConfigId | String | The ID after successful configuration. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=CreateDownStreamConfig
&FromUrl=rtmp://5000.liveplay.myqcloud.com/live/stream1
&ToUrl=rtmp://5000.livepush.myqcloud.com/live/stream2
&AreaId=1
&IspId=1
&StartTime=2018-12-31T11:02:00Z
&EndTime=2018-12-31T12:02:00Z
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ConfigId": "123",
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```


## 5. Developer Resources

### API Explorer

**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=CreateDownStreamConfig)

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
| InternalError.GetBizidError | Error getting user account. |
| InternalError.InvalidInput | Parameter check failed. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| MissingParameter | Missing parameter |

