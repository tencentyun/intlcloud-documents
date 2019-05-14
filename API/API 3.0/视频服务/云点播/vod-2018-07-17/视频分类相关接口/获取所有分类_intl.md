## 1. API Description
API domain name: vod.tencentcloudapi.com.
* This API gets the information of all categories.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeAllClass |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| ClassInfoSet | Array of [MediaClassInfo](/document/api/266/31773#MediaClassInfo) | Category information set <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Getting the Video Category Hierarchy
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeAllClass
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "ClassInfoSet": [
      {
        "ClassId": 0,
        "Level": 0,
        "ClassName": "Other",
        "ParentId": -1,
        "SubClassIdSet": null
      },
      {
        "ClassId": 1,
        "Level": 0,
        "ClassName": "Custom First-level Category",
        "ParentId": -1,
        "SubClassIdSet": [
          2,
          3
        ]
      },
      {
        "ClassId": 2,
        "Level": 2,
        "ClassName": "Custom Second-level Category",
        "ParentId": 1,
        "SubClassIdSet": [
          4,
          5
        ]
      },
      {
        "ClassId": 3,
        "Level": 2,
        "ClassName": "Custom Second-level Category",
        "ParentId": 1,
        "SubClassIdSet": null
      },
      {
        "ClassId": 4,
        "Level": 3,
        "ClassName": "Custom Third-level Category",
        "ParentId": 2,
        "SubClassIdSet": null
      },
      {
        "ClassId": 5,
        "Level": 3,
        "ClassName": "Custom Third-level Category",
        "ParentId": 2,
        "SubClassIdSet": null
      }
    ],
    "RequestId": "requestId"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeAllClass)
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
Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/266/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
| Error Code | Description |
|---------|---------|
| InternalError | Internal error |

