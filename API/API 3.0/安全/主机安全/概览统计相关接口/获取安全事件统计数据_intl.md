## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (DescribeSecurityTrends) is used to get the security event statistics.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeSecurityTrends. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| BeginDate | Yes | Date | Start time. |
| EndDate | Yes | Date | End time. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Malwares | Array of [SecurityTrend](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/296/19867#SecurityTrend) | Array of Trojan event statistics. |
| NonLocalLoginPlaces | Array of [SecurityTrend](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/296/19867#SecurityTrend) | Array of remote login event statistics. |
| BruteAttacks | Array of [SecurityTrend](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/296/19867#SecurityTrend) | Array of brute force attack event statistics. |
| Vuls | Array of [SecurityTrend](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/296/19867#SecurityTrend) | Array of vulnerability statistics. |
| BaseLines | Array of [SecurityTrend](https://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.comhttps://cloud.tencent.com/document/api/296/19867#SecurityTrend) | Array of baseline statistics. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Get security event statistics

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=DescribeSecurityTrends
&BeginDate=2018-10-08
&EndDate=2018-10-10
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "NonLocalLoginPlaces": [
      {
        "Date": "2018-10-08",
        "EventNum": 1
      },
      {
        "Date": "2018-10-09",
        "EventNum": 2
      },
      {
        "Date": "2018-10-10",
        "EventNum": 3
      }
    ],
    "Vuls": [
      {
        "Date": "2018-10-08",
        "EventNum": 1
      },
      {
        "Date": "2018-10-09",
        "EventNum": 2
      },
      {
        "Date": "2018-10-10",
        "EventNum": 3
      }
    ],
    "Malwares": [
      {
        "Date": "2018-10-08",
        "EventNum": 1
      },
      {
        "Date": "2018-10-09",
        "EventNum": 2
      },
      {
        "Date": "2018-10-10",
        "EventNum": 3
      }
    ],
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "BruteAttacks": [
      {
        "Date": "2018-10-08",
        "EventNum": 1
      },
      {
        "Date": "2018-10-09",
        "EventNum": 2
      },
      {
        "Date": "2018-10-10",
        "EventNum": 3
      }
    ],
    "BaseLines": [
      {
        "Date": "2018-10-08",
        "EventNum": 1
      },
      {
        "Date": "2018-10-09",
        "EventNum": 2
      },
      {
        "Date": "2018-10-10",
        "EventNum": 3
      }
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=DescribeSecurityTrends)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/296/19830#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.DateRange | Invalid time range format. |
| InvalidParameter.IllegalRequest | Invalid request. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |

