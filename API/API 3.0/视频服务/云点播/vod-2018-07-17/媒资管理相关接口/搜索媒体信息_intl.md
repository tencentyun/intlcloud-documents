## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API searches for media information and supports filtering and sorting the returned results in many ways. It can:
- Fuzzily search for text by media file name or description.
- Retrieve media files by category and tag.
    - Specify the category set "ClassIds" (see the input parameter) and return the media files in any category in the set. For example, assuming that there are categories of Movies, TV Series, and Variety Shows and there are subcategories of History, Action, and Romance in the category of Movies, if Movies and TV Series are specified in ClassIds, then all the subcategories under Movies and TV Series are returned.
    However, if History and Action are specified in ClassIds, only the media files in those two subcategories are returned.
    - Specify the tag set "Tags" (see the input parameter) and return the media files with any tag in the set. For example, assuming that there are tags of ACG, Drama, and YTPMV, if ACG and YTPMV are specified in Tags, then any media files with either tag are retrieved.
- Filter media files from a specified source (Source) (see the input parameter).
- Filter media files of LVB recording during LVB by LVB code of the push stream and Vid (see the input parameter).
- Filter media files by the creation time range.
- Mix and match any filters above to retrieve the media files that meet all the specified criteria. For example, you can filter the media files with the tag of Drama or YTPMV in the categories of Movies or TV Series created between December 1, 2018 and December 8, 2018
- Sort the results and return certain results by specifying the Offset and Limit.
API search limit:
- If there are over 5,000 search results, paged query is not supported for the excessive part.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: SearchMedia |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Text | No | String | Search text, which fuzzily matches the media file name or description. The more matching items and the higher the match rate, the higher-ranked the result. Length limit: 64 characters. |
| Tags.N | No | Array of String | Tag set, which matches any element in the set. <br/><li>Tag length limit: 8 characters. </li><li>Array length limit: 10.</li> |
| ClassIds.N | No | Array of Integer | Category ID set, which matches the categories of the specified IDs and all subcategories. Array length limit: 10. |
| StartTime | No | String | Start time in the creation time range. <br/><li>Before or at the start time. </li><li>In ISO 8601 format. For more information, see [Notes on ISO Date Format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). </li> |
| EndTime | No | String | End time in the creation time range. <br/><li>After the end time. </li><li>In ISO 8601 format. For more information, see [Notes on ISO Date Format](https://cloud.tencent.com/document/product/266/11732#iso-.E6.97.A5.E6.9C.9F.E6.A0.BC.E5.BC.8F). </li> |
| SourceType | No | String | Media file source. For the value range, see [SourceType](https://cloud.tencent.com/document/product/266/31773#MediaSourceData). |
| StreamId | No | String | [LVB code](https://cloud.tencent.com/document/product/267/5959) of the push stream. |
| Vid | No | String | Unique ID of the LVB recording file. |
| Sort | No | [SortBy](/document/api/266/31773#SortBy) | Sorting order. <br/><li>Sort.Field value range: CreateTime</li><li>If Text is specified for the search, the results are sorted by the match rate, and this field is invalid </li> |
| Offset | No | Integer | Offset. <br/><li>Default value: 0. </li><li>Value range: Offset + Limit cannot exceed 5,000. </li> |
| Limit | No | Integer | Number of returned entries; 10 by default. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of results matching the search criteria <br/><li>Maximum: 5,000, i.e., when the number of hits exceeds 5,000, this field returns 5,000 instead of the actual total hits. </li>|
| MediaInfoSet | Array of [MediaInfo](/document/api/266/31773#MediaInfo) | List of media file information, only including the basic information (BasicInfo) <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Searching for Media Information
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=SearchMedia
&Text=Test
&ClassIds.0=1
&ClassIds.1=2
&StartTime=2018-09-20T10:00:00Z
&EndTime=2018-10-02T10:00:00Z
&Sort.Field=CreatTime
&Sort.Order=Desc
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "MediaInfoSet": [
      {
        "FileId": "123",
        "BasicInfo": {
          "ClassId": 1,
          "ClassName": "Test",
          "ClassPath": "Test",
          "CoverUrl": "http://xx.vod2.myqcloud.com/xxxxxxxx/shotup/f0.100_0.jpg",
          "CreateTime": "2018-10-01T10:00:00Z",
          "Description": "",
          "ExpireTime": "2018-12-01T13:00:00Z",
          "Name": "test file",
          "MediaUrl": "http://xx.vod2.myqcloud.com/xx/xx/f0.mp4",
          "Type": "mp4",
          "TagSet": [],
          "StorageRegion": "ap-chongqing",
          "SourceInfo": {
            "SourceType": "Record",
            "SourceContext": "rtmp://3954.livepush2.myqcloud.com/live?anchor_type=1&bizid=3954&cert=d86fb5f28c35ecd3839b1790f5edb417&certTime=5c2570ad&pid=169258718_1545957549&publisher_rank=4&record=none&share_feeds=0&stemp_id=12345678&storage_time=15768000¡Áhift_bps=3000%7C1500¡Áhift_dur=86400&txAddTimestamp=4&txSecret=371e9e321a5acc063c2e96f766781e1a&txSeiUuid=EF68287DAFD64043A2F4007141781BEA&txTime=5c26c22d"
          },
          "Vid": "200025104_21313e19584d4b2a82af7c826581536c",
          "UpdateTime": "2018-10-01T13:10:03Z"
        }
      },
      {
        "FileId": "256",
        "BasicInfo": {
          "ClassId": 1,
          "ClassName": "Test",
          "ClassPath": "Test - Sports",
          "CoverUrl": "http://xx.vod2.myqcloud.com/xxxxxxxx/shotup/f0.100_0.jpg",
          "CreateTime": "2018-09-21T14:00:03Z",
          "Description": "",
          "ExpireTime": "2018-11-21T14:00:03",
          "Name": "test file2",
          "MediaUrl": "http://xx.vod2.myqcloud.com/xx/xx/f0.mp4",
          "Type": "mp4",
          "TagSet": [],
          "StorageRegion": "ap-chongqing",
          "SourceInfo": {
            "SourceType": "Record",
            "SourceContext": "rtmp://3954.livepush2.myqcloud.com/live?anchor_type=1&bizid=3954&cert=aa6af1917503f37781900fccbbf6755b&certTime=5c258827&pid=67180431_1545963559&publisher_rank=4&share_feeds=1&storage_mode=cold&storage_time=5184000&txSecret=d8c120c54fbf5b8e830437893c24a267&txTime=5c26d9a7"
          },
          "Vid": "1251883823_e247f6b09c5c4f168052355ce1e9c343",
          "UpdateTime": "2018-09-22T16:12:16Z"
        }
      }
    ],
    "RequestId": "requestId",
    "TotalCount": 2
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=SearchMedia)
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
| InternalError.GetMediaListError | Internal error: Error getting media list. |
| InvalidParameterValue.ClassIds | Incorrect parameter value: ClassIds is invalid. |
| InvalidParameterValue.EndTime | Incorrect parameter value: EndTime is invalid. |
| InvalidParameterValue.Offset | Incorrect parameter value: Offset is invalid. |
| InvalidParameterValue.Sort | Incorrect parameter value: Sort is invalid. |
| InvalidParameterValue.SourceType | Incorrect parameter value: SourceType is invalid. |
| InvalidParameterValue.StartTime | Incorrect parameter value: StartTime is invalid. |
| InvalidParameterValue.SubAppId | Incorrect parameter value: Sub-application ID |
| InvalidParameterValue.Tags | Incorrect parameter value: Tags is invalid. |
| InvalidParameterValue.Text | Incorrect parameter value: Search text. |
| LimitExceeded | Quota limit is exceeded. |

