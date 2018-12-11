## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API monitors the number of articles containing brand keywords that appear in public information channels such as Weibo, QQ Buluo, forums and blogs and outputs data results by date.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeBrandSocialReport |
| Version | Yes | String | Common parameter; its value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |
| StartDate | Yes | Date | Query start time |
| EndDate | Yes | Date | Query end time |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Cumulative statistics |
| DateCountSet | Array of [DateCount](/document/api/853/18402#DateCount) | Statistics by date |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Statistics on Social Media Reports of a Brand

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeBrandSocialReport
&BrandId=qijGLCi6bE0weVWgO7fjvfo4Wvo9kfzujw%3D%3D
&StartDate=2018-01-24
&EndDate=2018-02-01
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "DateCountSet": [
      {
        "Count": 98,
        "Date": "2018-01-24"
      },
      {
        "Count": 271,
        "Date": "2018-01-25"
      },
      {
        "Count": 402,
        "Date": "2018-01-26"
      },
      {
        "Count": 151,
        "Date": "2018-01-27"
      },
      {
        "Count": 481,
        "Date": "2018-01-28"
      },
      {
        "Count": 122,
        "Date": "2018-01-29"
      },
      {
        "Count": 206,
        "Date": "2018-01-30"
      },
      {
        "Count": 469,
        "Date": "2018-01-31"
      },
      {
        "Count": 33,
        "Date": "2018-02-01"
      }
    ],
    "RequestId": "6574337a-ac0a-4f5f-8b03-a6a3b8281040",
    "TotalCount": 2233
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeBrandSocialReport)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/853/18389#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.MetaDataOpFailed | Metadata operation failed. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Wrong parameter value |
| MissingParameter | Missing parameter |
| UnauthorizedOperation | Unauthorized operation |

