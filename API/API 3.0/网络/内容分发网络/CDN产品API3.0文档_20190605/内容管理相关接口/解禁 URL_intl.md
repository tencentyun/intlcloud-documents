## 1. API Description

API request domain name: cdn.tencentcloudapi.com.

EnableCaches is used to unblock manually blocked URLs. After a URL is successful unblocked, it takes about 5 to 10 minutes to take effect across the entire network. (This API is during beta test and not fully available now)

Default API request rate limit: 40 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/228/30977).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter, the value for this API: EnableCaches |
| Version | Yes | String | Common parameter, the value for this API: 2018-06-06 |
| Region | No | String | Common parameter; not passed in for this API. |
| Urls.N | Yes | Array of String | List of unblocked URLs |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CacheOptResult | [CacheOptResult](/document/api/228/30987#CacheOptResult) | Result list <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Unblocking a URL

#### Input Sample Code

```
https://cdn.tencentcloudapi.com/?Action=EnableCaches
&Urls.0=http://example.com/path/to.jpg
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "asdasdascsa721d8ha8chsa",
    "CacheOptResult": {
      "FailUrls": [],
      "SuccessUrls": [
        "http://example.com/path/to.jpg"
      ]
    }
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cdn&Version=2018-06-06&Action=EnableCaches)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/228/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CdnDbError | Internal data error. Please submit a ticket for troubleshooting. |
| InternalError.CdnSystemError | System error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CDNStatusInvalidDomain | Invalid domain name status |
| InvalidParameter.CdnHostInvalidParam | Invalid domain name format. Please check and try again. |
| InvalidParameter.CdnInterfaceError | Internal API error. Please submit a ticket for troubleshooting. |
| InvalidParameter.CdnParamError | Parameter error. Please see the sample parameters in the documentation. |
| InvalidParameter.CdnStatInvalidDate | Invalid date. Please see the sample date in the documentation. |
| InvalidParameter.CdnStatInvalidProjectId | Incorrect project ID. Please check and try again. |
| ResourceNotFound.CdnHostNotExists | This domain name does not exist under the account. Please check and try again. |
| ResourceNotFound.CdnUserNotExists | The CDN service has not been activated. Please activate it first before using this API. |
| UnauthorizedOperation.CdnAccountUnauthorized | The sub-account is unauthorized to query full data. |
| UnauthorizedOperation.CdnCamUnauthorized | No CAM policy is configured for the sub-account. |
| UnauthorizedOperation.CdnUserAuthFail | Fail to authenticate the CDN user. |
| UnauthorizedOperation.CdnUserAuthWait | The CDN user is pending authentication. |
| UnauthorizedOperation.CdnUserIsSuspended | The CDN service has been suspended. Please restart it and try again. |
| UnauthorizedOperation.CdnUserNoWhitelist | You are not in the beta whitelist and thus have no permission to use this function. |
