## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API returns the list of trending negative comments on a brand by analyzing the positive and negative sentiment scores of the words used in the comments.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeBrandNegComments |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |
| StartDate | Yes | Date | Query start time |
| EndDate | Yes | Date | Query end time |
| Limit | No | Integer | Maximum number of queried items; default value: 20 |
| Offset | No | Integer | Query offset, starting at 0 by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| BrandCommentSet | Array of [CommentInfo](/document/api/853/18402#CommentInfo) | Comment list |
| TotalComments | Integer | Total number of negative comments |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Brand Negative Comment List

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeBrandNegCommentList
&BrandId=qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujw%3D%3D
&StartDate=2018-02-21
&EndDate=2018-02-22
&Limit=10
&Offset=0
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "BrandCommentSet": [
      {
        "Comment": "No way! Is this OK?",
        "Date": "2018-02-22 00:00:00"
      },
      {
        "Comment": "I don't like it",
        "Date": "2018-02-22 00:00:00"
      },
      {
        "Comment": "It's too unsafe and basically ignores user requests",
        "Date": "2018-02-21 00:00:00"
      }
    ],
    "RequestId": "8fdd4c33-600c-4ec7-be16-c2cd4f6d4121",
    "TotalComments": 6
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeBrandNegComments)

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
| UnauthorizedOperation | Unauthorized operation |

