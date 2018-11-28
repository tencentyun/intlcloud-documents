## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API returns the number of positive and negative comments on a brand by analyzing the positive and negative sentiment scores of the words used in the comments and outputs the results by date.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeBrandCommentCount |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |
| StartDate | Yes | Date | Query start date |
| EndDate | Yes | Date | Query end date |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CommentSet | Array of [Comment](/document/api/853/18402#Comment) | Number of positive/negative comments by date |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Number of Brand Positive/negative Comments

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeBrandComments
&BrandId=qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujw%3D%3D
&StartDate=2018-01-02
&EndDate=2018-01-04
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "CommentSet": [
      {
        "Date": "2018-01-02",
        "NegCommentCount": 3,
        "PosCommentCount": 9
      },
      {
        "Date": "2018-01-03",
        "NegCommentCount": 1,
        "PosCommentCount": 5
      },
      {
        "Date": "2018-01-04",
        "NegCommentCount": 4,
        "PosCommentCount": 10
      }
    ],
    "RequestId": "1362f83b-c845-490e-bc81-49ee6ff8159b"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeBrandCommentCount)

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
| InternalError.InnerServerFailed | Internal API error. |
| InternalError.MetaDataOpFailed | Metadata operation failed. |
| InvalidParameter | Parameter error |
| UnauthorizedOperation | Unauthorized operation |

