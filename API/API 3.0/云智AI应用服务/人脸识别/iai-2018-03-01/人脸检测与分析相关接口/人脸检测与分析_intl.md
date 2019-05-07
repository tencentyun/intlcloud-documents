## 1. API Description

API request domain name: iai.tencentcloudapi.com.

This API detects the position, attributes, and quality information of the face in the given image. The position information includes (x, y, w, h); the face attributes include gender, age, expression, beauty, glass, hair, mask, and pose (pitch, roll, yaw); and the face quality information includes the overall quality score, sharpness, brightness, and completeness.

 
The face quality information is mainly used to evaluate the quality of the input face image. When using Face Recognition, you are recommended to evaluate the quality of the input face image first to improve the effects of subsequent processing. Application scenarios of this feature include:

1) [Creating](https://cloud.tencent.com/document/product/867/32793)/[adding](https://cloud.tencent.com/document/product/867/32795) a person in a group: This is to ensure the quality of the face information to facilitate subsequent processing.

2) [Face search](https://cloud.tencent.com/document/product/867/32798): This is to ensure the quality of the input image to quickly find the corresponding person.

3) [Face verification](https://cloud.tencent.com/document/product/867/32806): This is to ensure the quality of the face information to avoid cases where the verification incorrectly fails.

4) [Face fusion](https://cloud.tencent.com/product/facefusion): This is to ensure the quality of the uploaded face images to improve the fusion effect.



Default API request frequency limit: 50 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/867/32773).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DetectFace |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-01 |
| Region | No | String | Common parameter; not passed in for this API |
| MaxFaceNum | No | Integer | The maximum number of faces that can be processed. The default value is 1 (i.e., detecting only the face with the largest size in the image), and the maximum value is 30. <br/>This parameter is used to control the number of faces in the image to be detected. The smaller the value, the faster the processing. |
| MinFaceSize | No | Integer | The minimum height and width of the face in px. 40 by default. Faces below this size will not be detected. |
| Image | No | String | Base64 data of the image. Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |
| Url | No | String | Either the Url of Image of the image must be provided; if both are provided, only Url will be used. <br/>It is recommended to store the image in Tencent Cloud, as a Tencent Cloud URL can guarantee higher download speed and stability. <br/>The download speed and stability of non-Tencent Cloud URLs may be low. <br/>Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |
| NeedFaceAttributes | No | Integer | Whether to return the face attribute information (FaceAttributesInfo). 0 - no; 1 - yes. 0 by default. <br/>If the value is not 1, it is deemed not to return, and FaceAttributesInfo is meaningless in this case.  <br/>The face attribute information of up to 5 largest faces in the image will be returned, and FaceAttributesInfo of the 6th and rest faces is meaningless.  <br/>Extracting face attribute information is quite time-consuming. If face attribute information is not required, it is recommended to disable this feature to speed up face detection. |
| NeedQualityDetection | No | Integer | Whether to enable quality detection. 0 - disabled; 1 - enabled. 0 by default. <br/>If the value is not 1, it is deemed not to perform quality detection.  <br/>It is recommended to enable this feature for the face adding operation. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ImageWidth | Integer | Width of the requested image. |
| ImageHeight | Integer | Height of the requested image. |
| FaceInfos | Array of [FaceInfo](/document/api/867/32807#FaceInfo) | Face information list. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Sample 1. API for Face Detection and Analysis

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=DetectFace
&MaxFaceNum=1
&MinFaceSize=40
&Url=http://test.image.myqcloud.com/testA.jpg
&NeedFaceAttributes=1
&NeedQualityDetection=1
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ImageWidth": 640,
    "ImageHeight": 440,
    "FaceInfos": [
      {
        "X": 156,
        "Y": 129,
        "Width": 196,
        "Height": 196,
        "FaceAttributesInfo": {
          "Gender": 99,
          "Age": 51,
          "Expression": 99,
          "Hat": false,
          "Glass": false,
          "Mask": true,
          "Hair": {
            "Length": 1,
            "Bang": 1,
            "Color": 0
          },
          "Pitch": 17,
          "Yaw": 5,
          "Roll": -2,
          "Beauty": 71
        },
        "FaceQualityInfo": {
          "Score": 63,
          "Sharpness": 73,
          "Brightness": 47,
          "Completeness": {
            "Eyebrow": 99,
            "Eye": 99,
            "Nose": 99,
            "Cheek": 52,
            "Mouth": 99,
            "Chin": 47
          }
        }
      }
    ],
    "RequestId": "bcde47b5-e6d8-446e-a538-bcecffbe306a"
  }
}
```

### Sample 2. API for Face Detection and Analysis

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=DetectFace
&MaxFaceNum=1
&MinFaceSize=40
&Url=http://test.image.myqcloud.com/testB.jpg
&NeedFaceAttributes=0
&NeedQualityDetection=0
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ImageWidth": 640,
    "ImageHeight": 440,
    "FaceInfos": [
      {
        "X": 156,
        "Y": 129,
        "Width": 196,
        "Height": 196,
        "FaceAttributesInfo": {
          "Gender": 0,
          "Age": 0,
          "Expression": 0,
          "Hat": false,
          "Glass": false,
          "Mask": false,
          "Hair": {
            "Length": 0,
            "Bang": 0,
            "Color": 0
          },
          "Pitch": 0,
          "Yaw": 0,
          "Roll": 0,
          "Beauty": 0
        },
        "FaceQualityInfo": {
          "Score": 0,
          "Sharpness": 0,
          "Brightness": 0,
          "Completeness": {
            "Eyebrow": 0,
            "Eye": 0,
            "Nose": 0,
            "Cheek": 0,
            "Mouth": 0,
            "Chin": 0
          }
        }
      }
    ],
    "RequestId": "a574102d-1b86-48a7-a08b-6a741a8fedb6"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iai&Version=2018-03-01&Action=DetectFace)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/867/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.ConflictOperation | Operation conflict. Do not operate on the same person simultaneously. |
| FailedOperation.DuplicatedGroupDescription | The custom description field must be unique in the group. |
| FailedOperation.GroupInDeletedState | The current group is being deleted. Please wait. |
| FailedOperation.GroupPersonMapExist | The ID of the corresponding person is already in the group. |
| FailedOperation.GroupPersonMapNotExist | The ID of the corresponding person is not in the group. |
| FailedOperation.ImageDecodeFailed | Image decoding failed. |
| FailedOperation.ImageDownloadError | Error downloading the image. |
| FailedOperation.ImageFacedetectFailed | Face detection failed. |
| FailedOperation.ImageSizeExceed | Size of the Base64-encoded image cannot exceed 5 MB. |
| FailedOperation.RequestTimeout | Backend service timed out. |
| FailedOperation.SearchFacesExceed | The number of faces searched exceeds the limit. |
| FailedOperation.ServerError | The algorithm service is exceptional. Please retry. |
| InternalError | Internal error. |
| InvalidParameter.InvalidParameter | Invalid parameter. |
| InvalidParameterValue.AccountFaceNumExceed | The number of faces in the account exceeds the limit. There can be up to 10 million faces under one APPID. |
| InvalidParameterValue.DeleteFaceNumExceed | The number of faces to be deleted exceeds the limit. Every person must have at least one face image. |
| InvalidParameterValue.GroupExDescriptionsExceed | The array length of the group's custom description field exceeds the limit. Up to 5 ones can be created. |
| InvalidParameterValue.GroupExDescriptionsNameIdentical | The name of the group's custom description field must be unique. |
| InvalidParameterValue.GroupExDescriptionsNameIllegal | The name of the group's custom description field contains invalid characters. It can contain only Chinese characters, letters, -, _, and digits. |
| InvalidParameterValue.GroupExDescriptionsNameTooLong | The name of the group's custom description field exceeds the length limit. |
| InvalidParameterValue.GroupFaceNumExceed | The number of faces in the group exceeds the limit. One group can contain up to one million faces. |
| InvalidParameterValue.GroupIdAlreadyExist | The group ID already exists. It must be unique. |
| InvalidParameterValue.GroupIdIllegal | The group ID contains invalid characters. It can contain only letters, digits, and -%@#&_. |
| InvalidParameterValue.GroupIdNotExist | The group ID does not exist. |
| InvalidParameterValue.GroupIdTooLong | The group ID exceeds the length limit. |
| InvalidParameterValue.GroupIdsExceed | The list of groups passed in exceeds the limit. |
| InvalidParameterValue.GroupNameAlreadyExist | The group name already exists. It must be unique. |
| InvalidParameterValue.GroupNameIllegal | The group name contains invalid characters. It can contain only Chinese characters, letters, -, _, and digits. |
| InvalidParameterValue.GroupNameTooLong | The group name exceeds the length limit. |
| InvalidParameterValue.GroupNumExceed |  The number of groups exceeds the limit. Up to 20,000 ones can be created. If you need more, please contact us. |
| InvalidParameterValue.GroupNumPerPersonExceed | The number of groups exceeds the limit. One person can be added to up to 100 groups. |
| InvalidParameterValue.GroupTagIllegal | The group tag contains invalid characters. It can contain only Chinese characters, letters, -, _, and digits. |
| InvalidParameterValue.GroupTagTooLong | The group tag exceeds the length limit. |
| InvalidParameterValue.ImageEmpty | The image is empty. |
| InvalidParameterValue.LimitExceed | The number of returns exceeds the limit. |
| InvalidParameterValue.NoFaceInGroups | There are no faces in the specified group. |
| InvalidParameterValue.NoFaceInPhoto | There are no faces in the image. |
| InvalidParameterValue.OffsetExceed | The starting number is too large. Please check the length of the array to be requested. |
| InvalidParameterValue.PersonExDescriptionInfosExceed | The array length of the person's custom description field exceeds the limit. Up to 5 ones are allowed. |
| InvalidParameterValue.PersonExDescriptionsNameIdentical | The name of the person's custom description field must be unique. |
| InvalidParameterValue.PersonExDescriptionsNameIllegal | The name of the person's custom description field contains invalid characters. It can contain only Chinese characters, letters, -, _, and digits. |
| InvalidParameterValue.PersonExDescriptionsNameTooLong | The name of the person's custom description field exceeds the length limit. |
| InvalidParameterValue.PersonExistInGroup | The ID of the corresponding person is already in the group. |
| InvalidParameterValue.PersonFaceNumExceed | The number of faces for the person exceeds the limit. One person can have up to five face images. |
| InvalidParameterValue.PersonGenderIllegal |  Error with the set person gender. 0 - blank; 1 - male; 2 - female. |
| InvalidParameterValue.PersonIdAlreadyExist | The person ID already exists. The person ID must be unique. |
| InvalidParameterValue.PersonIdIllegal | The person ID contains invalid characters. It can contain only letters, digits, and -%@#&_. |
| InvalidParameterValue.PersonIdNotExist | The person ID does not exist. |
| InvalidParameterValue.PersonIdTooLong | The person ID exceeds the length limit. |
| InvalidParameterValue.PersonNameIllegal | The person name contains invalid characters. The person name can contain only Chinese characters, letters, -, _, and digits. |
| InvalidParameterValue.PersonNameTooLong | The person name exceeds the length limit. |
| InvalidParameterValue.SearchPersonsExceed | The number of persons searched exceeds the limit. |
| InvalidParameterValue.UploadFaceNumExceed | Up to four faces can be uploaded at a time. |
| InvalidParameterValue.UrlIllegal | Invalid URL format. |
| LimitExceeded.ErrorFaceNumExceed | The number of faces exceeds the limit. |
| MissingParameter.ErrorParameterEmpty | A required parameter is empty. |
| ResourceUnavailable.Delivering | The resource is being delivered. |
| ResourceUnavailable.Freeze | The account has been frozen. |
| ResourceUnavailable.InArrears | The account is in arrears. |
| ResourceUnavailable.NotExist | The billing status is unknown. Please check whether the service has been activated in the console. |
| ResourceUnavailable.Recover | The resource has been reclaimed. |
| ResourceUnavailable.StopUsing | The service has been stopped for the account. |
| ResourceUnavailable.UnknownStatus | The billing status is unknown. |
| ResourcesSoldOut.ChargeStatusException | The billing status is exceptional. |
| UnsupportedOperation.UnknowMethod | Unknown method name. |

