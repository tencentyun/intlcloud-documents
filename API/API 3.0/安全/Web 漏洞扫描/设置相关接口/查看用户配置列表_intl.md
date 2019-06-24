## 1. API Description
API request domain name: cws.tencentcloudapi.com.

This API (DescribeConfig) is used to query the details of the user configuration.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/692/16736).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeConfig |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-12 |
| Region | No | String | Common parameter; not passed in for this API |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| NoticeLevel | String | Notification level for vulnerability alarm with 4 digits representing high risk, medium risk, low risk and notice respectively. |
| Id | Integer | Configuration ID. |
| CreatedAt | Timestamp | Creation time of the record. |
| UpdatedAt | Timestamp | Last update time of the record. |
| Appid | Integer | Tencent Cloud user's appid. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing User Configuration List

#### Input

```
https://cws.tencentcloudapi.com/?Action=DescribeConfig
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "Appid": 1251001047,
    "CreatedAt": "2018-03-20T20:30:56+08:00",
    "Id": 1,
    "NoticeLevel": "1110",
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "UpdatedAt": "2018-03-24T15:24:10+08:00"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer)

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

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/692/16738#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |

