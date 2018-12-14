## 1. API Description

API request domain name: tbm.tencentcloudapi.com.

This API monitors the appearances of brand keywords in article titles and bodies on media websites (such as news websites, web portals, government websites, WeChat Official Accounts and kb.qq.com) and outputs the results by date.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/853/18387).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeBrandMediaReport |
| Version | Yes | String | Common parameter; the value for this API: 2018-01-29 |
| Region | No | String | Common parameter; not passed in for this API |
| BrandId | Yes | String | Brand ID |
| StartDate | Yes | Date | Query start time |
| EndDate | Yes | Date | Query end time |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of articles in the query range |
| DateCountSet | Array of [DateCount](/document/api/853/18402#DateCount) | Number of daily articles by date |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Number of Brand News Reports

#### Input Example

```
https://tbm.tencentcloudapi.com/?Action=DescribeBrandMediaReport
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
        "Count": 600,
        "Date": "2018-01-24"
      },
      {
        "Count": 3231,
        "Date": "2018-01-25"
      },
      {
        "Count": 10030,
        "Date": "2018-01-26"
      },
      {
        "Count": 32,
        "Date": "2018-01-27"
      },
      {
        "Count": 48,
        "Date": "2018-01-28"
      },
      {
        "Count": 17,
        "Date": "2018-01-29"
      },
      {
        "Count": 75,
        "Date": "2018-01-30"
      },
      {
        "Count": 3195,
        "Date": "2018-01-31"
      },
      {
        "Count": 694,
        "Date": "2018-02-01"
      }
    ],
    "RequestId": "b8edf4f1-5d24-493c-b51b-95ff681b218f",
    "TotalCount": 17922
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tbm&Version=2018-01-29&Action=DescribeBrandMediaReport)

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

