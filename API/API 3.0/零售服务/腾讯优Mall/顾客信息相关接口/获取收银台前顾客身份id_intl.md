## 1. API Description

API request domain name: youmall.tencentcloudapi.com.

This API gets the headshots and IDs of visitors captured by the cashier camera with the specified device ID in the specified time period.

Default API request frequency limit: 20 times/second.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/860/18451).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; its value for this API: DescribeCameraPerson |
| Version | Yes | String | Common parameter; its value for this API: 2018-02-28 |
| Region | No | String | Common parameter; not passed in for this API |
| CompanyId | Yes | String | Company ID in YouMall; obtained using the DescribeShopInfo API |
| ShopId | Yes | Integer | Shop ID in YouMall; obtained using the DescribeShopInfo API |
| CameraId | Yes | Integer | Camera ID |
| StartTime | Yes | Integer | Pull start timestamp in seconds |
| EndTime | Yes | Integer | Pull end timestamp in seconds; less than StartTime+10 seconds; if greater, defaulted to StartTime+10 |
| PosId | No | String | POS terminal ID |
| Num | No | Integer | Number of images pulled; default value: 1; maximum value: 3 |
| IsNeedPic | No | Integer | Whether a Base64-encoded image is required; 0 - not required, 1 - required, default value: 0 |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| CompanyId | String | Company ID |
| ShopId | Integer | Shop ID |
| CameraId | Integer | Camera ID |
| PosId | String | POS terminal ID |
| Infos | Array of [CameraPersonInfo](/document/api/860/18465#CameraPersonInfo) | Information of the captured visitors |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Getting Images Captured by Camera

#### Input Example

```
https://youmall.tencentcloudapi.com/?Action=DescribeCameraPerson
&CompanyId=tencent
&ShopId=10086
&CameraId=11
&PosId=test
&StartTime=1536743684
&EndTime=1536743686
&Num=4
&IsNeedPic=0
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "CameraId": 11,
    "CompanyId": "tencent",
    "Infos": [
      {
        "FaceId": 0,
        "FacePic": "",
        "IdType": 2,
        "TempId": "tencent_10086_11_20180912171447_2753739885041997564_1072_887_91_105",
        "Time": 1536743684
      },
      {
        "FaceId": 0,
        "FacePic": "",
        "IdType": 2,
        "TempId": "tencent_10086_11_20180912171537_2753740732643727005_1072_887_91_105",
        "Time": 1536743684
      }
    ],
    "PosId": "test",
    "RequestId": "07079dc5-5a08-4298-9aa8-6733cd940a05",
    "ShopId": 10086
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=youmall&Version=2018-02-28&Action=DescribeCameraPerson)

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

Only the error codes related to the API are listed below. For other error codes, see [Common Error Codes](/document/api/860/18453#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.NoData | No data. |
| FailedOperation.ParameterError | Error processing request parameters. |
| FailedOperation.ProcessFail | Processing failed. |

