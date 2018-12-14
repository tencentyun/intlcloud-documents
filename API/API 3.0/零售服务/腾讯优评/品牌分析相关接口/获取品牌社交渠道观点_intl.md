## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API detects articles containing brand keywords that appear in public information channels such as Weibo, QQ Buluo, forums and blogs and aggregates the list of opinions with the highest buzz in the past 30 days.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeBrandSocialOpinion |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |
| StartDate | Yes | Date | Retrieval start time |
| EndDate | Yes | Date | Retrieval end time |
| Offset | No | Integer | Query offset, starting at 0 by default |
| Limit | No | Integer | Maximum number of queried items; default value: 20 |
| ShowList | No | Boolean | List display tag; if true, article list details returned |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ArticleCount | Integer | Total number of articles |
| FromCount | Integer | Total number of sources |
| AdverseCount | Integer | Total number of suspected negative reports |
| ArticleSet | Array of [BrandReportArticle](/document/api/853/18402#BrandReportArticle) | Article list details |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Brand User Opinion List

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeBrandSocialOpinion
&BrandId=qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujw%3D%3D
&StartDate=2018-02-01
&EndDate=2018-02-10
&Offset=0
&Limit=1
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "AdverseCount": 2,
    "ArticleCount": 31,
    "ArticleSet": [
      {
        "Abstract": "Abstract",
        "ArticleId": "qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujwoo",
        "Flag": 0,
        "FromSite": "",
        "Hot": 1,
        "Level": 2,
        "PubTime": "2018-02-10 13:00:00",
        "Title": "test",
        "Url": ""
      }
    ],
    "FromCount": 1,
    "RequestId": "aaf3c86d-c143-4476-af5b-4d89ebc0f410"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeBrandSocialOpinion)

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

Only the error codes related to the API are listed below. For other error codes, see [Common Error Codes](/document/api/853/18389#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.MetaDataOpFailed | Metadata operation failed. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Wrong parameter value |
| MissingParameter | Missing parameter |
| UnauthorizedOperation | Unauthorized operation |

