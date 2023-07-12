## Feature Description
This feature can recognize all fields on the front and back of a second-generation Chinese ID card, including name, gender, ethnicity, date of birth, address, ID number, issuing authority, and validity period. It can also crop ID card photos and face photos, as well as warn about photographed, doctored, and photocopied images, edge and frame occlusions, temporary ID cards, and invalid validity periods.

>?
>- Currently, the ID card recognition feature has the following image requirements: the image cannot exceed 7 MB after being Base64-encoded. A resolution above 500x800 is recommended. PNG, JPG, JPEG, and BMP image are supported. We recommend that the card part occupy more than 2/3 area of the image.
>- ID card recognition is a paid service. For billing details, see Content Recognition Fees.
>- This feature currently can be used only through APIs.

## Request

#### Processing during upload
The request for recognizing ID cards during image upload is the same as that used to simply upload a file to COS, except that you need to add the relevant processing parameter. Then, the recognition results will be returned during image upload, and the input images can be stored in COS.

```plaintext
PUT /<ObjectKey>?ci-process=IDCardOCR&CardSide=<CardSide>&Config=<Config> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Processing in-cloud data
This feature can process an ID card image stored in COS and return the recognition result.

```plaintext
GET /<ObjectKey>?ci-process=IDCardOCR&CardSide=<CardSide>&Config=<Config> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request parameters

| Parameter | Description | Type | Required |
| ------------ | ------------------------------------------------------------ | ------- | -------- |
| ObjectKey | Object name, such as `folder/document.jpg`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `IDCardOCR` for ID card recognition. | String | Yes |
| CardSide | <li>FRONT: The side of the ID card with the face (face side)<br><li>BACK: The side of the ID card with the national emblem (national emblem side)<br> If this parameter is not specified, the system will automatically determine the ID card's front and back sides. | String | No |
| Config | The following fields are all of `bool` type and default to `false`:<br><li>CropIdCard: Crops the ID card photo (by removing extra edges outside the ID card and automatically correcting the shooting angle)<br><li>CropPortrait: Crops the face photo (by automatically cutting out the face area in the ID card)<br><li>CopyWarn: Warns about photocopied images<br><li>BorderCheckWarn: Warns about border and frame occlusions<br><li>ReshootWarn: Warns about spoofed images<br><li>DetectPsWarn: Warns about doctored images<br><li>TempIdWarn: Warns about temporary ID cards<br><li>InvalidDateWarn: Warns about invalid ID card validity periods<br><li>Quality: Gets the image quality score (by evaluating the blurriness of the image )<br><li>MultiCardDetect: Enables multi-card detection<br>For the parameter setting method, see <br>Config = {"CropIdCard":true,"CropPortrait":true}. | String | No |



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <IdInfo>
    Recognized ID card information
  </IdInfo>
  <AdvancedInfo>
    Recognized ID card information
  </AdvancedInfo>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :----- |
| IdInfo | Response | Recognized ID card information. | Container |
| AdvancedInfo | Response | Extended information, which will not be returned if not requested. | Container |

`IdInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :----- |
| Name | IdInfo | Name (face side) | String |
| Sex | IdInfo | Gender (face side) | String |
| Nation | IdInfo | Ethnicity (face side) | String |
| Birth | IdInfo | Date of birth (face side) | String |
| Address | IdInfo | Address (face side) | String |
| IdNum | IdInfo | ID number (face side) | String |
| Authority | IdInfo | Issuing authority (national emblem side) | String |
| ValidDate | IdInfo | Validity period (national emblem side) | String |

`AdvancedInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :----- |
| IdCard | AdvancedInfo | Base64-encoded content of the cropped ID card photo, which will be returned if `Config.CropIdCard` is set to `true`. | String |
| Portrait | AdvancedInfo | Base64-encoded content of the face on the ID card, which will be returned if `Config.CropPortrait` is set to `true`. | String |
| Quality | AdvancedInfo | Image quality score, which will be returned if `Config.Quality` is set to `true`. Value range: 0–100. The lower the score, the blurrier the image. The recommended threshold is ≥ 50. | String |
| BorderCodeValue | AdvancedInfo | Alarm threshold score for incomplete ID card borders, which will be returned if `Config.BorderCheckWarn` is set to `true`. Value range: 0–100. The lower the score, the lower the probability of border occlusion. The recommended threshold value is ≥ 50. | String |
| WarnInfos | IdInfo | Warning information. `Code` values and descriptions: <br><li>9100: The ID card validity period is invalid. <br><li>9101: The ID card borders are incomplete. <br><li>9102: The ID card image is photocopied. <br><li>9103: The ID card image is spoofed. <br><li>9104: The ID card is a temporary one. <br><li>9105: The ID card frame is occluded.<br><li>9106: The ID card image is doctored. <br>There may be multiple `WarnInfos` values. | String |

## Samples

#### Request

```plaintext
GET /test.jpg?ci-process=IDCardOCR&CardSide=FRONT&Config={"CropIdCard":true, "CropIdCard":true} HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 414641
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-image
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <IdInfo>
     <Name>Li Ming</Name>
     <Sex>Male</Sex>
     <Nation>Han</Nation>
     <Birth>1987/1/1</Birth>
     <Address>Tencent Building, Hi-tech Park, Shijingshan District, Beijing</Address>
     <IdNum>440524198701010014</IdNum>
  </IdInfo>
  <AdvancedInfo>
     <IdCard>Base64-encoded content of the cropped ID card photo</IdCard>
     <Portrait>Base64-encoded content of the face on the ID card</Portrait>
  </AdvancedInfo>
</Response>
```


## Error Codes

The following only lists the error codes for the business logic of this API. For other errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

| Error Code | Description |
| :----------------- | :------- |
| FailedOperation.DownLoadError | Failed to download the file. |
| FailedOperation.EmptyImageError | The image is empty. |
| FailedOperation.IdCardInfoIllegal | The ID card information is invalid (ID number, name, etc.). |
| FailedOperation.ImageBlur | The image is blurry. |
| FailedOperation.ImageDecodeFailed | Failed to decode the image. |
| FailedOperation.ImageNoIdCard | No ID card is detected in the image. |
| FailedOperation.ImageSizeTooLarge | The image is too large. See the description of image size limit in the output parameters. |
| FailedOperation.MultiCardError | There are multiple cards in the photo. |
| FailedOperation.OcrFailed | OCR failed. |
| FailedOperation.UnKnowError | An unknown error occurred. |
| FailedOperation.UnOpenError | The service has not been activated. |
| InvalidParameter.ConfigFormatError | The `Config` format is incorrect. |
| InvalidParameterValue.InvalidParameterValueLimit | The parameter value is incorrect. |
| LimitExceeded.TooLargeFileError | The file is too large. |
| ResourcesSoldOut.ChargeStatusException | The billing status is abnormal. |

