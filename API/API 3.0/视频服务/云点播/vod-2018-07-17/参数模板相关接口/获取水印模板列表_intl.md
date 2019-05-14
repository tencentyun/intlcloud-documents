## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API queries custom watermarking templates and supports paged queries by filters.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeWatermarkTemplates |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Definitions.N | No | Array of Integer | Unique ID filter of the watermarking template; array length limit: 100. |
| Type | No | String | Filter of watermark type; value range: <br/><li>image: Image watermark; </li><li>text: Text watermark. </li> |
| Offset | No | Integer | Paged offset; 0 by default. |
| Limit | No | Integer | Number of returned entries <br/><li>Default value: 10; </li><li>Maximum value: 100.</li> |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible entries. |
| WatermarkTemplateSet | Array of [WatermarkTemplate](/document/api/266/31773#WatermarkTemplate) | List of watermarking template details. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Getting a Watermarking Template
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=DescribeWatermarkTemplates
&Definitions.0=1001
&Offset=0
&Limit=20
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "TotalCount": 1,
    "WatermarkTemplateSet": {
      "Definition": 1001,
      "Type": "image",
      "Name": "Sample Structured to Be Improved",
      "Comment": "Test template",
      "XPos": "10%",
      "YPos": "10%",
      "ImageTemplate": {
        "ImageUrl": "http://1256768367.vod2.myqcloud.com/8b0dd2b5vodcq1256768367/4d27b39f5285890783754292994/aa.jpeg",
        "Width": "80%",
        "Height": "80%"
      },
      "TextTemplate": {
        "FontType": "arial.ttf",
        "FontSize": "16px",
        "FontColor": "0xFF0000",
        "FontAlpha": 1
      },
      "CreateTime": "2018-10-01T10:00:00Z",
      "UpdateTime": "2018-10-01T10:00:00Z"
    },
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeWatermarkTemplates)
### SDK
TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.
* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
### TCCLI
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)
## 6. Error Codes
Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/266/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).
| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue.Definitions | Incorrect parameter value: Definitions. |
| InvalidParameterValue.Limit | Parameter error: Limit. |
| InvalidParameterValue.Type | Incorrect Type parameter value. |

