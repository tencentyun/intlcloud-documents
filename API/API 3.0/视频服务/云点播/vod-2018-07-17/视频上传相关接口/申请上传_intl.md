## 1. API Description
API domain name: vod.tencentcloudapi.com.
* This API is used to apply for uploading a media file (and cover file) to Tencent Cloud VOD and obtain the metadata of file storage (including upload path and upload signature) for subsequent use by the uploading API.
* For the detailed upload process, see [Server Upload Overview](https://cloud.tencent.com/document/product/266/9759#.E4.B8.8A.E4.BC.A0.E6.B5.81.E7.A8.8B).
Default API request rate limit: 100 requests/sec.
Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as vod.ap-shanghai-fsi.tencentcloudapi.com.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ApplyUpload |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/266/31756#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| MediaType | Yes | String | Media type. For the detailed value range, see [Upload Overview](https://cloud.tencent.com/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B). |
| MediaName | No | String | Media name. |
| CoverType | No | String | Cover type. For the detailed value range, see [Upload Overview](https://cloud.tencent.com/document/product/266/9760#.E6.96.87.E4.BB.B6.E7.B1.BB.E5.9E.8B). |
| Procedure | No | String | Subsequent task for the media. For more information, see [Upload-specific Task Flow](https://cloud.tencent.com/document/product/266/9759). |
| ExpireTime | No | Timestamp | Expiry time of the media file in ISO 8601 format. For more information, see [Notes on ISO Date Format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). |
| StorageRegion | No | String | Specify the upload region. This is only applicable to users that have special requirements for the upload region. |
| ClassId | No | Integer | Category ID, which is used to categorize the media for management. A category can be created and its ID can be obtained by using the [category creating](https://cloud.tencent.com/document/product/266/7812) API. <br/><li>Default value: 0, which means "Other". </li> |
| SourceContext | No | String | The source context which is used to pass through the user request information. The upload callback API returns the value of this field. Up to 250 characters. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| StorageBucket | String | Bucket, which is used as the bucket_name of the URL in the uploading API. |
| StorageRegion | String | Storage region, which is used as the Region of the Host in the uploading API. |
| VodSessionKey | String | VOD session, which is used to confirm the VodSessionKey parameter in the uploading API. |
| MediaStoragePath | String | Media storage path, which is used as the Key of the media storage in the uploading API. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| CoverStoragePath | String | Cover storage path, which is used as the Key of the cover storage in the uploading API. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| TempCertificate | [TempCertificate](/document/api/266/31773#TempCertificate) | Temporary credential, which is used for authentication in the uploading API. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
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
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ApplyUpload)
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
| InvalidParameter.ExpireTime | Incorrect parameter value: Expiry time. |
| InvalidParameterValue.CoverType | Incorrect parameter value: Cover type. |
| InvalidParameterValue.MediaType | Incorrect parameter value: Media type. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |

