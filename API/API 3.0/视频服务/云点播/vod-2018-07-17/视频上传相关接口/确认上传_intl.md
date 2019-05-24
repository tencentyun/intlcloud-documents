## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API confirms that the a media file (and cover file) is successfully uploaded to Tencent Cloud VOD, stores the file information, and returns the playback address and the media file ID.  
Default API request rate limit: 100 requests/sec.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi),  you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| VodSessionKey | Yes | String | VOD session, same as the value of VodSessionKey returned by the file-uploading application API. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| FileId | String | Unique ID of the media file. |
| MediaUrl | String | Media playback address. <br/>Note: Null means no valid values returned. |
| CoverUrl | String | Media cover address. <br/>Note: Null means no valid values returned.|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

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
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents)

### SDK
TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.
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
| InternalError | The error is caused internally. |
| InvalidParameterValue.VodSessionKey | The VOD session is invalid. |
| ResourceNotFound | The specified resource does not exist or is not found. |


