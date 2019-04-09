## 1. API Description

API request domain name: live.tencentcloudapi.com.

After a watermark is added and a watermark ID is successfully returned, you need to call the [CreateLiveWatermarkRule](/document/product/267/32629) API and bind the watermark ID to the stream.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/267/20459).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: AddLiveWatermark |
| Version | Yes | String | Common parameter; the value for this API: 2018-08-01 |
| Region | No | String | Common parameter; not passed in for this API |
| PictureUrl | Yes | String | Watermark image URL |
| WatermarkName | Yes | String | Watermark name |
| XPosition | No | Integer | Display position; X-axis offset |
| YPosition | No | Integer | Display position; Y-axis offset |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| WatermarkId | Integer | Watermark ID |
| RequestId | String | The unique request ID which is returned for each request The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Request Sample

#### Input Sample Code

```
https://live.tencentcloudapi.com/?Action=AddLiveWatermark
&PictureUrl=http://watermark-10005041.cos.myqcloud.com/1251830167/watermark_img_Alogo.png
&XPosition=80
&YPosition=10
&WatermarkName=logo
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03",
    "WatermarkId":123
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=live&Version=2018-08-01&Action=AddLiveWatermark)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

