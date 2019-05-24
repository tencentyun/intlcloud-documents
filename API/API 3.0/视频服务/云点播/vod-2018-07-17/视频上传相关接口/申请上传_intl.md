## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API applies for uploading a media file (and cover file) to Tencent Cloud VOD and returns metadata (including uploading path and signature) for future file-uploading requests.  
* For the detailed uploading process, see [Server Upload Overview](https://cloud.tencent.com/document/product/266/9759#.E4.B8.8A.E4.BC.A0.E6.B5.81.E7.A8.8B).

Default API request rate limit: 100 requests/sec.  

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi),  you need to specify a domain name with the financial availability zone as well, which preferably in the same region as the specified Region, for example: vod.ap-shanghai-fsi.tencentcloudapi.com.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| MediaType | Yes | String | Media type. For valid values, see [Upload Overview](https://cloud.tencent.com/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B). |
| MediaName | No | String | Media name. |
| CoverType | No | String | Cover type. For valid values, see [Upload Overview](https://cloud.tencent.com/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B). |
| Procedure | No | String | Subsequent tasks. For more information, see [Upload-specific Task Flow](https://cloud.tencent.com/document/product/266/9759). |
| ExpireTime | No | Timestamp | Expiration time of the media file in ISO 8601 format. For more information, see [Notes on ISO Date Format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| StorageRegion | No | String | Specify the upload region when needed. |
| ClassId | No | Integer | Category ID, used to manage the media resources. You can create a category and its ID using API [category creating](https://cloud.tencent.com/document/product/266/7812) <br/><li>Default value: 0, indicating "Other". </li> |
| SourceContext | No | String | The source context passed along with the request. The upload callback API will return this value. Maximum 250 characters allowed. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| StorageBucket | String | Bucket, which is used as the bucket_name of the URL in the uploading API. |
| StorageRegion | String | Storage region, which is used as the Region of the Host in the uploading API. |
| VodSessionKey | String | VOD session, which is used to confirm the VodSessionKey parameter in the uploading API. |
| MediaStoragePath | String | Media storage path, which is used as the Key of the media storage in the uploading API. <br/>Note: Null means no valid values returned. |
| CoverStoragePath | String | Cover storage path, which is used as the Key of the cover storage in the uploading API. <br/>Note: Null means no valid values returned. |
| TempCertificate | [TempCertificate](/document/api/266/31773#TempCertificate) | Temporary credentials used for API request authentication. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Successful Application for Upload
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ApplyUpload
&MediaType=mp4
&SubAppId=1
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "CoverStoragePath": null,
    "RequestId": "880f3005-a8c9-4bba-8c87-74e216a17a0b",
    "StorageBucket": "xadagzp111211-100922",
    "StorageRegion": "ap-guangzhou-2",
    "MediaStoragePath": "/dir/name.xx",
    "VodSessionKey": "VodSessionKey",
    "TempCertificate": {
      "SecretId": "xxxxxxx",
      "SecretKey": "xxxxxxxx",
      "Token": "xxxxxxxx",
      "ExpiredTime": 182823331
    }
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
| InvalidParameter.ExpireTime | Invalid value specified in the parameter: The time typed is passed. |
| InvalidParameterValue.CoverType | The specified cover type is unsupported . |
| InvalidParameterValue.MediaType | The specified media type is unsupported. |
| InvalidParameterValue.SubAppId | The sub-application ID is invalid or unfounded. |


