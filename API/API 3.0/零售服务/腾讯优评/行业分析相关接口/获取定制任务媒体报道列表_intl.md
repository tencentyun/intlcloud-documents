## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API monitors the appearances of customized industry keywords in article titles and bodies on media websites (such as news websites, web portals, government websites, WeChat Official Accounts and kb.qq.com) as well as the article lists, source channels, authors and release time.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeIndustryNews |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| IndustryId | Yes | String | Industry ID |
| StartDate | Yes | Date | Query start time |
| EndDate | Yes | Date | Query end time |
| ShowList | No | Boolean | Whether to display the list; if true, article list returned |
| Offset | No | Integer | Query offset, starting at 0 by default |
| Limit | No | Integer | Maximum number of queried items; default value: 20 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| NewsCount | Integer | Total number of articles |
| FromCount | Integer | Total number of sources |
| AdverseCount | Integer | Total number of suspected negative articles |
| NewsSet | Array of [IndustryNews](/document/api/853/18402#IndustryNews) | Article list |
| DateCountSet | Array of [DateCount](/document/api/853/18402#DateCount) | Count by date |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Customized Industry-related Reports

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeIndustryNews
&IndustryId=qijGLCi6bE0weVWrJ7L4qgm5nxET0u0Y9XwF
&StartDate=2018-02-1
&EndDate=2018-02-10
&Offset=1
&Limit=1
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "AdverseCount": 2,
    "DateCountSet": [
      {
        "Count": 3,
        "Date": "2018-07-07"
      },
      {
        "Count": 0,
        "Date": "2018-07-08"
      },
      {
        "Count": 0,
        "Date": "2018-07-09"
      },
      {
        "Count": 2,
        "Date": "2018-07-10"
      }
    ],
    "FromCount": 1,
    "NewsCount": 152,
    "NewsSet": [
      {
        "Abstract": "Abstract",
        "Flag": 0,
        "FromSite": "qieguang-zb",
        "Hot": 1,
        "Level": 2,
        "PubTime": "2018-02-09 10:32:07",
        "Title": "Understand the New Retail Ecosystem Layouts of Alibaba and Tencent in Three Images",
        "Url": "http://mp.weixin.qq.com/s?__biz=MzI1MzczMDQzNg==&mid=2247483907&idx=1&sn=91deced0aff67a2143bc3cbccbfae0a6&chksm=e9d149e8dea6c0fe661426638396a05fb7fc5c8adf5cac07157f93e31d2613483b196ddd754d#rd"
      }
    ],
    "RequestId": "02363e3b-b048-40df-aaeb-8ec0f449e525"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeIndustryNews)

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

