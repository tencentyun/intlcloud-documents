## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API queries and sorts custom watermark templates by page.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeWatermarkTemplates |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Definitions.N | No | Array of Integer | Unique filter of the watermark template; array length limit: 100. |
| Type | No | String | Filter of watermark type; value range: <br/><li>image: Image watermark; </li><li>text: Text watermark. </li> |
| Offset | No | Integer | Paged offset; 0 by default. |
| Limit | No | Integer | Number of returned entries <br/><li>Default value: 10; </li><li>Maximum value: 100.</li> |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible entries. |
| WatermarkTemplateSet | Array of [WatermarkTemplate](/document/api/266/31773#WatermarkTemplate) | List of watermark template details. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Getting a Watermark Template
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
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=DescribeWatermarkTemplates)

### SDK
TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.
* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes
The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/267/20461#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | The error is caused internally. |
| InvalidParameterValue.Definition | The value of *Definitions* is invalid. |
| InvalidParameterValue.Limit | The value of *Limit* is invalid. |
| InvalidParameterValue.Type | The specified watermark type is invalid. |

