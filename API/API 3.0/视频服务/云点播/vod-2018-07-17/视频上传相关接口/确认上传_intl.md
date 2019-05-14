## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API is used to confirm the result of uploading a media file (and cover file) to Tencent Cloud VOD, store the media information, and return the playback address and ID of the media file.
Default API request rate limit: 100 requests/sec.
Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as vod.ap-shanghai-fsi.tencentcloudapi.com.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CommitUpload |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| VodSessionKey | Yes | String | VOD session, which takes the return value (VodSessionKey) of the upload applying API. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| FileId | String | Unique ID of the media file. |
| MediaUrl | String | Media playback address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverUrl | String | Media cover address. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample1. Successful Upload
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CommitUpload
&VodSessionKey=3KEGq9DWHl1xF819mM4jVFkGn5WON80NwN/rTrx56UoEFApIV9DQ7t5m1g4hASR11gKWwGxkignB3AmhKOpUnym7wyNEHOwDJPcT5fBu66iCLcW7bhyRfDSsQcVpX0Wt96RKSsZFf62jeAB+e5640U8rMPV3Rf2eR+y1AgI+EC3JZU5iZbjLX4qNVI4R&SubAppId=1
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "FileId": "24820810452266399",
    "MediaUrl": "http://251000333.vod2.myqcloud.com/6c0f1c00vodgzp251000333/dee2125c24820810452266399/f0.mp4",
    "CoverUrl": "http://251000333.vod2.myqcloud.com/6c0f1c00vodgzp251000333/dee2125c24820810452266399/24820810452266400.jpg",
    "RequestId": "requestId"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=CommitUpload)
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
| InvalidParameterValue.VodSessionKey | Incorrect parameter value: VOD session. |
| ResourceNotFound | Resource does not exist. |

