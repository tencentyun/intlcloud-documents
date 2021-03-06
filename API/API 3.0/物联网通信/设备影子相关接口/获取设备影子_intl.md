## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (DescribeDeviceShadow) is used to query the information of virtual devices.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](https://cloud.tencent.com/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeDeviceShadow |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| ProductId | Yes | String | Product ID |
| DeviceName | Yes | String | Device name. Naming rule: [a-zA-Z0-9:_-]{1,48} |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Data | String | Device shadow data |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting a Device Shadow

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=DescribeDeviceShadow
&ProductId=ABCDE12345
&DeviceName=abc
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "Data": "{\"payload\":{\"state\": {\"reported\": { \"color\": \"red\"}}, \"metadata\": {\"reported\": {\"color\": {\"timestamp\": 1509092895971}}}, \"timestamp\": 1509443636326, \"version\": 5},\"result\":0,\"timestamp\":1509440846582,\"type\":\"get\"}",
    "RequestId": "xxxxxxxxxxxxxxxxxxxxxxx"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=DescribeDeviceShadow)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/634/19474#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.ParamIncomplete | Key field information missing in the request. |
| ResourceNotFound.DeviceShadowNotExist | Device shadow does not exist. |
| ResourceNotFound.ProductOrDeviceNotExist | This product or device does not exist for the user. |
