## 1. API Description

API request domain name: ocr.tencentcloudapi.com.

The API for identity card recognition supports the recognition of all fields on the front and back of a second-generation Chinese ID card, including name, gender, ethnicity, date of birth, address, citizen ID number, issuing authority and validity period, and features ID card/portrait photo cropping and photocopied/photographed ID cards detection. Application scenarios include verification of ID card information validity for bank account opening, user registration and face recognition.

Default API request frequency limit: 20 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/866/33518).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: IDCardOCR |
| Version | Yes | String | Common parameter; the value for this API: 2018-11-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/866/33518#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| ImageBase64 | No | String | Base64 value of the image. <br/>Supported image formats: PNG, JPG, JPEG; GIF is not supported at present. <br/>Supported image size: The downloaded image cannot exceed 6 MB in size after Base64 encoding. The image download time cannot exceed 3 seconds. <br/>Either the ImageUrl or ImageBase64 of the image must be provided; if both are provided, only ImageBase64 will be used. |
| ImageUrl | No | String | URL of the image. <br/>Supported image formats: PNG, JPG, JPEG; GIF is not supported at present. <br/>Supported image size: The downloaded image cannot exceed 3 MB in size after Base64 encoding. The image download time cannot exceed 3 seconds. <br/>It is recommended to store the image in Tencent Cloud, as a Tencent Cloud URL can guarantee higher download speed and stability. The download speed and stability of non-Tencent Cloud URLs may be low. |
| CardSide | No | String | FRONT is the side on the ID card containing the photo (front) <br/>BACK is the side on the ID card containing the national emblem (back) |
| Config | No | String | Optional field; this is to select whether to request the corresponding fields as needed. Currently, the fields included: <br/>CropIdCard - ID card photo cropping, <br/>CropPortrait - portrait photo cropping, <br/>CopyWarn - warning for photocopied ID card, <br/>ReshootWarn - warning for reshot ID card. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Name | String | Name (front) |
| Sex | String | Gender (front) |
| Nation | String | Ethnicity (front) |
| Birth | String | Date of birth (front) |
| Address | String | Address (front) |
| IdNum | String | ID number (front) |
| Authority | String | Issuing authority (back) |
| ValidDate | String | Validity period (back) |
| AdvancedInfo | String | Extended information, which returns the corresponding information for the optional fields of the request and dose not return if not requested. Currently, supported extended fields include: <br/>IdCard - ID card photo, returned if CropIdCard is requested; <br/>Portrait - portrait photo, returned if CropPortrait is requested; <br/>WarnInfos - warning message (Code - warning code, Msg - warning message), returned if photocopied or reshot ID card is recognized. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Sample Codes

### 1. Sample Code for ID Card Recognition (Front)

#### Input Sample

```
https://ocr.tencentcloudapi.com/?Action=IDCardOCR
&ImageUrl=https://xx/a.jpg 
&CardSide=FRONT
&<Common request parameter>
```

#### Output Sample

```
{
    "Response": {
        "Name": "李明",
        "Sex": "男",
        "Nation": "汉",
        "Birth": "1987/1/1",
        "Address": "北京市石景山区高新技术园腾讯大楼",
        "IdNum": "440524198701010014",
        "Authority": "",
        "ValidDate": "",
        "AdvancedInfo": "{}",
        "RequestId": "ab2c132e-9e1c-43d3-b0ef-9b4d80f00330"
    }
}
```

### 2. Sample Code for ID Card Recognition (Back)

#### Input Sample

```
https://ocr.tencentcloudapi.com/?Action=IDCardOCR
&ImageUrl=https://xx/a.jpg 
&CardSide=BACK
&<Common request parameter>
```

#### Output Sample

```
{
    "Response": {
        "Name": "",
        "Sex": "",
        "Nation": "",
        "Birth": "",
        "Address": "",
        "IdNum": "",
        "Authority": "赵县公安局",
        "ValidDate": "2010.07.21-2020.07.21",
        "AdvancedInfo": "{}",
        "RequestId": "0d394478-6d4d-48fc-8b19-552415bf46de"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=ocr&Version=2018-11-19&Action=IDCardOCR)

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
| FailedOperation.ImageBlur | The photo is blurry |
| FailedOperation.ImageDecodeFailed | Image decoding failed |
| FailedOperation.ImageNoIdCard | No ID card detected in the photo |
| FailedOperation.ImageSizeTooLarge | The image size is too large |
| FailedOperation.OcrFailed | OCR failed |
| FailedOperation.UnKnowError | Unknown error |
| FailedOperation.UnOpenError | The service is not activated |
| InvalidParameter.ConfigFormatError | Config is not in valid JSON format |
| InvalidParameterValue.InvalidParameterValueLimit | Wrong parameter value |
| LimitExceeded.TooLargeFileError | The file is too large |
| ResourcesSoldOut.ChargeStatusException | Abnormal billing status |
