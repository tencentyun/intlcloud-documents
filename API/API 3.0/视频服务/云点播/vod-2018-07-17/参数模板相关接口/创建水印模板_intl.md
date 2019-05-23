## 1. API Description
API domain name: vod.tencentcloudapi.com.  
This API creates up to 1000 custom watermark template.  
Default API request rate limit: 100 requests/sec.

## 2. Input Parameters
The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/266/31756).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ModifyTranscodeTemplate |
| Version | Yes | String | Common parameter; the version of this API: 2018-07-17 |
| Region | No | String | Common parameter; optional for this API |
| Type | Yes | String | Watermark type: <br/><li>image: Image watermark; </li><li>text: Text watermark. </li> |
| Name | No | String | The name of the watermark template (maximum 64 characters). |
| Comment | No | String | The description of the template (maximum 256 bytes). |
| CoordinateOrigin | No | String | Origin position: <br/><li>TopLeft: The origin of coordinates is in the top-left corner of the video, and the origin of the watermark is in the top-left corner of the image or text; </li><li>TopRight: The origin of coordinates is in the top-right corner of the video, and the origin of the watermark is in the top-right corner of the image or text; </li><li>BottomLeft: The origin of coordinates is in the bottom-left corner of the video, and the origin of the watermark is in the bottom-left corner of the image or text; </li><li>BottomRight: The origin of coordinates is in the bottom-right corner of the video, and the origin of the watermark is in the bottom-right corner of the image or text. </li><br/>Default value: TopLeft. Currently, if Type is image, this field supports only TopLeft. |
| XPos | No | String | The horizontal position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported: <br/><li>If the string ends in %, the left edge of the watermark is at the position of the specified percentage of the video width, for example, 10% means that the left edge is at 10% of the video width; </li><li>if the string ends in px, the left edge of the watermark is at the position of the specified px of the video width, for example, 100px means that the left edge is at the position of 100px. </li><br/>Default value: 0px. |
| YPos | No | String | The vertical position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported: <br/><li>If the string ends in %, the top edge of the watermark is at the position of the specified percentage of the video height, for example, 10% means that the top edge is at 10% of the video height; </li><li>if the string ends in px, the top edge of the watermark is at the position of the specified px of the video height, for example, 100px means that the top edge is at the position of 100px. </li><br/>Default value: 0px. |
| ImageTemplate | No | [ImageWatermarkInput](/document/api/266/31773#ImageWatermarkInput) | Image watermark template. This field is required if Type is image. It is invalid if Type is text. |
| TextTemplate | No | [TextWatermarkTemplateInput](/document/api/266/31773#TextWatermarkTemplateInput) | Text watermark template. This field is required if Type is text. It is invalid if Type is image. |
| SvgTemplate | No | [SvgWatermarkInput](/document/api/266/31773#SvgWatermarkInput) | SVG watermark template. This field is required if Type is svg. It is invalid if Type is image or text. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). Input the ID of the sub-application that has the desired resources; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| Definition | Integer | Unique ID of the watermark template. |
| ImageUrl | String | Watermark image address. This field is valid only when the watermark type is image. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample
### Sample 1. Creating a Watermark Template
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=CreateWatermarkTemplate
&Type=image
&Name=Template 1
 
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "Definition": 1001,
    "ImageUrl": "http://1256768367.vod2.myqcloud.com/8b0dd2b5vodcq1256768367/4d27b39f5285890783754292994/aa.jpeg",
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```
## 5. Developer Resources
### API Explorer
**API Explorer is a tool that provides ease of use in requesting APIs, authenticating identities, generating SDK and exploring APIs in Tencent Cloud environment.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=PullEvents)

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
| InternalError.UploadWatermarkError | Failed to upload a watermark. |
| InvalidParameterValue | A value specified in a parameter is not valid or cannot be used for this request. |
| InvalidParameterValue.Comment | The description of the template is invalid. |
| InvalidParameterValue.CoordinateOrigin | The coordinates of the origin are invalid. |
| InvalidParameterValue.Height | The value of the video height is invalid. |
| InvalidParameterValue.ImageTemplate | The watermark template is unsupported |
| InvalidParameterValue.Name | The length of the name exceeds the limit. |
| InvalidParameterValue.TextAlpha | The input value of the text transparency is incorrect or invalid. |
| InvalidParameterValue.TextTemplate | The text template is invalid. |
| InvalidParameterValue.Type | The input value of the type is invalid. |
| InvalidParameterValue.Width | The specified video width is invalid. |
| InvalidParameterValue.XPos | The input value of Xpos is invalid. XPos is the horizontal coordinate of the watermark origin relative to the video origin coordinates. % and px are the supported units. |
| InvalidParameterValue.YPos | The input value of Xpos is invalid. YPos is the vertical coordinate of the watermark origin relative to the video origin coordinates. % and px are the supported units. |
| LimitExceeded.TooMuchTemplate | The number of templates exceeds the limit. |

