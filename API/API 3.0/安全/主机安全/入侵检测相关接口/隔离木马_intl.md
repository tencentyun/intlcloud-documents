## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (SeparateMalwares) is used to isolate Trojans.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: SeparateMalwares. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| Ids.N | Yes | Array of Integer | Array of Trojan event IDs. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| SuccessIds | Array of Integer | Array of IDs of Trojans successfully isolated. |
| FailedIds | Array of Integer | Array of IDs of Trojans that failed to be isolated. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Isolate Trojans

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=SeparateMalwares
&Ids.0=123
&Ids.1=456
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "FailedIds": [],
    "RequestId": "4985eb7f-62d6-4da8-898f-d92a08660a38",
    "SuccessIds": [
      123,
      456
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=SeparateMalwares)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/296/19830#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.PartSeparate | Some of the hosts failed to be isolated. |
| FailedOperation.SingleSeparate | Failed to isolate a single host. |
| InternalError | Internal error. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |
| InvalidParameter.MissingParameter | Missing parameter. |
| InvalidParameter.ParsingError | Parameter parsing error. |

