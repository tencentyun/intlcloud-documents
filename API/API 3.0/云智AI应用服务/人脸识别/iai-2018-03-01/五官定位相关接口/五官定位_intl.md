## 1. API Description

API request domain name: iai.tencentcloudapi.com.

This API performs facial feature localization (aka facial key point localization) on a given image and calculate 90 facial key points that make up the contour of the face, including eyebrows (8 points on the left and 8 on the right), eyes (8 points on the left and 8 on the right), nose (13 points), mouth (22 points), face contour (21 points), and eyeballs [or pupils] (2 points).

Default API request frequency limit: 50 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/867/32773).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: AnalyzeFace |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-01 |
| Region | No | String | Common parameter; not passed in for this API |
| Mode | No | Integer | Detection mode. 0 - detect all faces that appear; 1 - detect the largest face. 0 by default. The facial feature localization information (facial key points) of up to 10 faces can be returned. |
| Image | No | String | Base64 data of the image. Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |
| Url | No | String | Either the Url of Image of the image must be provided; if both are provided, only Url will be used.  <br/>It is recommended to store the image in Tencent Cloud, as a Tencent Cloud URL can guarantee higher download speed and stability. <br/>The download speed and stability of non-Tencent Cloud URLs may be low. <br/>Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ImageWidth | Integer | Width of the requested image. |
| ImageHeight | Integer | Height of the requested image. |
| FaceShapeSet | Array of [FaceShape](/document/api/867/32807#FaceShape) | Specific information of facial feature localization (facial key points). |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### API for Facial Feature Localization

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=AnalyzeFace
&Mode=0
&Url=http://test.image.myqcloud.com/testA.jpg
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ImageWidth": 550,
    "ImageHeight": 366,
    "FaceShapeSet": [
      {
        "FaceProfile": [
          {
            "X": 63,
            "Y": 335
          },
          {
            "X": 63,
            "Y": 374
          },
          {
            "X": 66,
            "Y": 412
          },
          {
            "X": 74,
            "Y": 450
          },
          {
            "X": 85,
            "Y": 487
          },
          {
            "X": 100,
            "Y": 522
          },
          {
            "X": 121,
            "Y": 554
          },
          {
            "X": 147,
            "Y": 582
          },
          {
            "X": 176,
            "Y": 608
          },
          {
            "X": 208,
            "Y": 627
          },
          {
            "X": 245,
            "Y": 634
          },
          {
            "X": 282,
            "Y": 627
          },
          {
            "X": 315,
            "Y": 607
          },
          {
            "X": 344,
            "Y": 582
          },
          {
            "X": 370,
            "Y": 554
          },
          {
            "X": 391,
            "Y": 522
          },
          {
            "X": 405,
            "Y": 487
          },
          {
            "X": 416,
            "Y": 449
          },
          {
            "X": 423,
            "Y": 411
          },
          {
            "X": 427,
            "Y": 372
          },
          {
            "X": 426,
            "Y": 334
          }
        ],
        "LeftEye": [
          {
            "X": 114,
            "Y": 333
          },
          {
            "X": 128,
            "Y": 345
          },
          {
            "X": 146,
            "Y": 349
          },
          {
            "X": 165,
            "Y": 347
          },
          {
            "X": 183,
            "Y": 341
          },
          {
            "X": 169,
            "Y": 325
          },
          {
            "X": 150,
            "Y": 318
          },
          {
            "X": 130,
            "Y": 321
          }
        ],
        "RightEye": [
          {
            "X": 378,
            "Y": 331
          },
          {
            "X": 364,
            "Y": 343
          },
          {
            "X": 345,
            "Y": 348
          },
          {
            "X": 327,
            "Y": 346
          },
          {
            "X": 309,
            "Y": 340
          },
          {
            "X": 322,
            "Y": 323
          },
          {
            "X": 341,
            "Y": 316
          },
          {
            "X": 361,
            "Y": 319
          }
        ],
        "LeftEyeBrow": [
          {
            "X": 79,
            "Y": 280
          },
          {
            "X": 108,
            "Y": 275
          },
          {
            "X": 138,
            "Y": 274
          },
          {
            "X": 168,
            "Y": 277
          },
          {
            "X": 198,
            "Y": 279
          },
          {
            "X": 173,
            "Y": 256
          },
          {
            "X": 139,
            "Y": 251
          },
          {
            "X": 105,
            "Y": 256
          }
        ],
        "RightEyeBrow": [
          {
            "X": 410,
            "Y": 277
          },
          {
            "X": 380,
            "Y": 273
          },
          {
            "X": 350,
            "Y": 272
          },
          {
            "X": 320,
            "Y": 275
          },
          {
            "X": 290,
            "Y": 277
          },
          {
            "X": 315,
            "Y": 255
          },
          {
            "X": 349,
            "Y": 249
          },
          {
            "X": 384,
            "Y": 254
          }
        ],
        "Mouth": [
          {
            "X": 173,
            "Y": 522
          },
          {
            "X": 193,
            "Y": 541
          },
          {
            "X": 217,
            "Y": 554
          },
          {
            "X": 244,
            "Y": 558
          },
          {
            "X": 272,
            "Y": 554
          },
          {
            "X": 297,
            "Y": 541
          },
          {
            "X": 317,
            "Y": 522
          },
          {
            "X": 291,
            "Y": 517
          },
          {
            "X": 264,
            "Y": 512
          },
          {
            "X": 245,
            "Y": 517
          },
          {
            "X": 225,
            "Y": 512
          },
          {
            "X": 199,
            "Y": 517
          },
          {
            "X": 196,
            "Y": 528
          },
          {
            "X": 220,
            "Y": 532
          },
          {
            "X": 244,
            "Y": 535
          },
          {
            "X": 269,
            "Y": 532
          },
          {
            "X": 293,
            "Y": 528
          },
          {
            "X": 293,
            "Y": 525
          },
          {
            "X": 269,
            "Y": 527
          },
          {
            "X": 245,
            "Y": 530
          },
          {
            "X": 221,
            "Y": 528
          },
          {
            "X": 197,
            "Y": 525
          }
        ],
        "Nose": [
          {
            "X": 244,
            "Y": 428
          },
          {
            "X": 245,
            "Y": 341
          },
          {
            "X": 231,
            "Y": 367
          },
          {
            "X": 217,
            "Y": 392
          },
          {
            "X": 203,
            "Y": 418
          },
          {
            "X": 187,
            "Y": 448
          },
          {
            "X": 217,
            "Y": 464
          },
          {
            "X": 245,
            "Y": 468
          },
          {
            "X": 272,
            "Y": 464
          },
          {
            "X": 302,
            "Y": 448
          },
          {
            "X": 287,
            "Y": 417
          },
          {
            "X": 273,
            "Y": 392
          },
          {
            "X": 259,
            "Y": 366
          }
        ],
        "LeftPupil": [
          {
            "X": 188,
            "Y": 303
          }
        ],
        "RightPupil": [
          {
            "X": 201,
            "Y": 304
          }
        ]
      }
    ],
    "RequestId": "a8eb4545-a154-4f86-9510-57a8be9cae0c"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iai&Version=2018-03-01&Action=AnalyzeFace)

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

