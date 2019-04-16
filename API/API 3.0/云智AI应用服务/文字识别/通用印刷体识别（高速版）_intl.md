## 1. API Description

API request domain name: ocr.tencentcloudapi.com.

The API for general printed text recognition (hi-speed version) is used to provide detection and recognition services for characters in images and returns the text box positions and characters. Compared to the API for general printed text recognition, this API features higher recognition speed and supported QPS.

Default API request frequency limit: 20 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/866/33518).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: GeneralFastOCR |
| Version | Yes | String | Common parameter; the value for this API: 2018-11-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/866/33518#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| ImageBase64 | No | String | Base64 value of the image. <br/>Supported image formats: PNG, JPG, JPEG; GIF is not supported at present. <br/>Supported image size: The downloaded image cannot exceed 3 MB in size after Base64 encoding. The image download time cannot exceed 3 seconds. <br/>Either the ImageUrl or ImageBase64 of the image must be provided; if both are provided, only ImageBase64 will be used. |
| ImageUrl | No | String | URL of the image. <br/>Supported image formats: PNG, JPG, JPEG; GIF is not supported at present. <br/>Supported image size: The downloaded image cannot exceed 3 MB in size after Base64 encoding. The image download time cannot exceed 3 seconds. <br/>It is recommended to store the image in Tencent Cloud, as a Tencent Cloud URL can guarantee higher download speed and stability. The download speed and stability of non-Tencent Cloud URLs may be low. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TextDetections | Array of [TextDetection](/document/api/866/33527#TextDetection) | Recognized text; for more information, click the link on the left |
| Language | String | Detected language; currently, the following languages are supported: Simplified Chinese, Traditional Chinese, English, Japanese and Korean. More languages will be supported in the future. <br/>Meaning of the return result: zh - Chinese/English; jap - Japanese; kor - Korean. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Sample Codes

### 1. Sample Code for General Printed Text Recognition (Hi-speed Version)

#### Input Sample

```
https://ocr.tencentcloudapi.com/?Action=GeneralFastOCR
&ImageUrl=https://xx/a.jpg
&<Common request parameter>
```

#### Output Sample

```
{
    "Response": {
        "TextDetections": [
            {
                "DetectedText": "原装进口",
                "Confidence": 99,
                "Polygon": null,
                "AdvancedInfo": "{\"Parag\":{\"ParagNo\":1}}"
            },
            {
                "DetectedText": "丝滑柔密泡沫",
                "Confidence": 99,
                "Polygon": null,
                "AdvancedInfo": "{\"Parag\":{\"ParagNo\":2}}"
            },
            {
                "DetectedText": "滋润感up",
                "Confidence": 99,
                "Polygon": null,
                "AdvancedInfo": "{\"Parag\":{\"ParagNo\":2}}"
            },
            {
                "DetectedText": "添加丝胶蛋白成分",
                "Confidence": 99,
                "Polygon": null,
                "AdvancedInfo": "{\"Parag\":{\"ParagNo\":3}}"
            },
            {
                "DetectedText": "添加美容液成分",
                "Confidence": 99,
                "Polygon": null,
                "AdvancedInfo": "{\"Parag\":{\"ParagNo\":3}}"
            }
        ],
        "Language": "zh",
        "RequestId": "1ac786b7-eedd-42a8-9df1-22be965fbb2d"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ocr&Version=2018-11-19&Action=GeneralFastOCR)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/866/33521#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.DownLoadError | File download failed |
| FailedOperation.EmptyImageError | The image is empty |
| FailedOperation.ImageDecodeFailed | Image decoding failed |
| FailedOperation.ImageNoText | No text detected in the image |
| FailedOperation.LanguageNotSupport | The input language is not supported |
| FailedOperation.OcrFailed | OCR failed |
| FailedOperation.UnKnowError | Unknown error |
| FailedOperation.UnOpenError | The service is not activated |
| InvalidParameterValue.InvalidParameterValueLimit | Wrong parameter value |
| LimitExceeded.TooLargeFileError | The file is too large |
| ResourcesSoldOut.ChargeStatusException | Abnormal billing status |
