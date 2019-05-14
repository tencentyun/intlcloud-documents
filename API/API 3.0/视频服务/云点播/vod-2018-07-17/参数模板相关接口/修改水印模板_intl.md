## 1. API Description
API domain name: vod.tencentcloudapi.com.
This API modifies a customer watermarking template. The watermark type cannot be modified.
Default API request rate limit: 100 requests/sec.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/266/31756).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ModifyWatermarkTemplate |
| Version | Yes | String | Common parameter; the value for this API: 2018-07-17 |
| Region | No | String | Common parameter; not passed in for this API |
| Definition | Yes | Integer | Unique ID of the watermarking template. |
| Name | No | String | Watermarking template name of up to 64 characters. |
| Comment | No | String | Template description of up to 256 characters. |
| CoordinateOrigin | No | String | Origin position; value range: <br/><li>TopLeft: The origin of coordinates is in the top-left corner of the video, and the origin of the watermark is in the top-left corner of the image or text; </li><li>TopRight: The origin of coordinates is in the top-right corner of the video, and the origin of the watermark is in the top-right corner of the image or text; </li><li>BottomLeft: The origin of coordinates is in the bottom-left corner of the video, and the origin of the watermark is in the bottom-left corner of the image or text; </li><li>BottomRight: The origin of coordinates is in the bottom-right corner of the video, and the origin of the watermark is in the bottom-right corner of the image or text. </li><br/>Currently, if Type is image, this field supports only TopLeft. |
| XPos | No | String | The horizontal position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported: <br/><li>If the string ends in %, the left edge of the watermark is at the position of the specified percentage of the video width, for example, 10% means that the left edge is at 10% of the video width; </li><li>if the string ends in px, the left edge of the watermark is at the position of the specified px of the video width, for example, 100px means that the left edge is at the position of 100px. </li> |
| YPos | No | String | The vertical position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported: <br/><li>If the string ends in %, the top edge of the watermark is at the position of the specified percentage of the video height, for example, 10% means that the top edge is at 10% of the video height; </li><li>if the string ends in px, the top edge of the watermark is at the position of the specified px of the video height, for example, 100px means that the top edge is at the position of 100px. </li> |
| ImageTemplate | No | [ImageWatermarkInputForUpdate](/document/api/266/31773#ImageWatermarkInputForUpdate) | Image watermarking template. This field is valid only for an image watermarking template. |
| TextTemplate | No | [TextWatermarkTemplateInputForUpdate](/document/api/266/31773#TextWatermarkTemplateInputForUpdate) | Text watermarking template. This field is valid only for a text watermarking template. |
| SvgTemplate | No | [SvgWatermarkInputForUpdate](/document/api/266/31773#SvgWatermarkInputForUpdate) | SVG watermarking template. This field is required if Type is svg. It is invalid if Type is image or text. |
| SubAppId | No | Integer | ID of the VOD [sub-application](/document/product/266/14574). If you need to access a resource in a sub-application, enter the sub-application ID in this field; otherwise, leave it blank. |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| ImageUrl | String | Image watermark address. This field has a value only when ImageTemplate.ImageContent is non-empty. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |
## 4. Sample
### Sample 1. Modifying a Watermarking Template
#### Input Sample Code
```
https://vod.tencentcloudapi.com/?Action=ModifyWatermarkTemplate
&Definition=1001
&Name=Template 2
&<Common request parameter>
```
#### Output Sample Code
```
{
  "Response": {
    "ImageUrl": null,
    "RequestId": "12ae8d8e-dce3-4151-9d4b-5594145287e1"
  }
}
```
## 5. Developer Resources
### API Explorer
**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=vod&Version=2018-07-17&Action=ModifyWatermarkTemplate)
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
| InternalError.UploadWatermarkError | Internal error: Watermark image upload failed. |
| InvalidParameterValue | Incorrect parameter value. |
| InvalidParameterValue.Comment | Parameter error: Template description. |
| InvalidParameterValue.CoordinateOrigin | Parameter error: CoordinateOrigin. |
| InvalidParameterValue.Height | Parameter error: Height. |
| InvalidParameterValue.Name | Parameter error: Name exceeds the length limit. |
| InvalidParameterValue.RepeatType | Incorrect parameter value: RepeatType is invalid. |
| InvalidParameterValue.TextAlpha | Parameter error: Text transparency. |
| InvalidParameterValue.Type | Incorrect Type parameter value. |
| InvalidParameterValue.Width | Parameter error: Width. |
| InvalidParameterValue.XPos | The horizontal position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported. |
| InvalidParameterValue.YPos | The vertical position of the origin of the watermark relative to the origin of coordinates of the video. % and px formats are supported. |
| ResourceNotFound | Resource does not exist. |

