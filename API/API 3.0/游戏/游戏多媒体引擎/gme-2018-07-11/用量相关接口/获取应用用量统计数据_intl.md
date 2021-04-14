## 1. API Description

API domain name: gme.tencentcloudapi.com.

This API (DescribeAppStatistics) is used to get the usage statistics of a GME application, including those of voice chat, voice messaging and speech-to-text, phrase filtering, etc. The maximum query period is the past 30 days.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/607/35367).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAppStatistics |
| Version | Yes | String | Common parameter. The value used for this API: 2018-07-11 |
| Region | No | String | Common parameter. This parameter is not required for this API |
| BizId | Yes | Integer | GME application ID |
| StartDate | Yes | Date | Data start date (GMT+8) in the format of yyyy-mm-dd, such as 2018-07-13 |
| EndDate | Yes | Date | Data end date (GMT+8) in the format of yyyy-mm-dd, such as 2018-07-13 |
| Services.N | Yes | Array of String | List of services to be queried. Value range: RealTimeSpeech, VoiceMessage, VoiceFilter |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AppStatistics | Array of [AppStatisticsItem](https://cloud.tencent.com/document/api/607/35375#AppStatisticsItem) | Application usage statistics |

## 4. Samples

### Sample 1. Querying the Usage Statistics of Voice Chat and Voice Messaging and Speech-to-text Between August 1 and August 3, 2019

#### Input Sample Code

```
https://gme.tencentcloudapi.com/?Action=DescribeAppStatistics
&BizId=140000001
&StartDate=2019-08-01
&EndDate=2019-08-03
&Services.0=RealTimeSpeech
&Services.1=VoiceMessage
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Data": {
      "AppStatistics": [
        {
          "Date": "2019-08-01",
          "RealtimeSpeechStatisticsItem": {
            "MainLandDau": 10000,
            "MainLandPcu": 5000,
            "MainLandDuration": 1000000,
            "OverseaDau": 5000,
            "OverseaPcu": 2000,
            "OverseaDuration": 500000
          },
          "VoiceMessageStatisticsItem": {
            "Dau": 68000
          },
          "VoiceFilterStatisticsItem": null
        },
        {
          "Date": "2019-08-02",
          "RealtimeSpeechStatisticsItem": {
            "MainLandDau": 10000,
            "MainLandPcu": 5000,
            "MainLandDuration": 1000000,
            "OverseaDau": 5000,
            "OverseaPcu": 2000,
            "OverseaDuration": 500000
          },
          "VoiceMessageStatisticsItem": {
            "Dau": 68000
          },
          "VoiceFilterStatisticsItem": null
        },
        {
          "Date": "2019-08-03",
          "RealtimeSpeechStatisticsItem": {
            "MainLandDau": 10000,
            "MainLandPcu": 5000,
            "MainLandDuration": 1000000,
            "OverseaDau": 5000,
            "OverseaPcu": 2000,
            "OverseaDuration": 500000
          },
          "VoiceMessageStatisticsItem": {
            "Dau": 68000
          },
          "VoiceFilterStatisticsItem": null
        }
      ]
    },
    "RequestId": "9b993045-9fa1-47f4-9d25-79160f305be8"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=gme&Version=2018-07-11&Action=DescribeAppStatistics)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/607/35370#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidParameter | Invalid parameter. |
| InvalidParameter.DateInvalid | Invalid date. |
| InvalidParameter.TimeRangeError | Incorrect query time range. |
| ResourceNotFound | Resource does not exist. |
| ResourceNotFound.BizidIsNotFound | Application ID does not exist. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
