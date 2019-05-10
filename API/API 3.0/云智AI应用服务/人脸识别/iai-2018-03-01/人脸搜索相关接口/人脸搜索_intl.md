## 1. API Description

API request domain name: iai.tencentcloudapi.com.

This API recognizes top N persons in one or more people libraries who are similar to the person in a given image and rank the similarity in a descending order. It supports up to one million faces in one single search.
This API should be used together with the [group management APIs](https://cloud.tencent.com/document/product/867/32794).

Default API request frequency limit: 50 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/867/32773).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: SearchFaces |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-01 |
| Region | No | String | Common parameter; not passed in for this API |
| GroupIds.N | Yes | Array of String | The list of groups to be searched in; up to 100 ones. |
| Image | No | String | Base64 data of the image. Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |
| Url | No | String | Either the Url of Image of the image must be provided; if both are provided, only Url will be used. <br/>It is recommended to store the image in Tencent Cloud, as a Tencent Cloud URL can guarantee higher download speed and stability. <br/>The download speed and stability of non-Tencent Cloud URLs may be low. <br/>Images in .png, .jpg, .jpeg, and .bmp but not .gif formats are supported. |
| MaxFaceNum | No | Integer | The maximum number of faces that can be processed. The default value is 1 (i.e., detecting only the face with the largest size in the image), and the maximum value is 10. <br/>MaxFaceNum is used to control the number of faces to be searched if there are multiple faces in the image. <br/>If MaxFaceNum is not 1 but M, search for M:N faces is performed actually. |
| MinFaceSize | No | Integer | The minimum height and width of the face in px. 80 by default. If it is below 40, the search accuracy will be compromised. It is recommended to set it at 80. |
| MaxPersonNum | No | Integer | Faces detected, corresponding to the maximum number of returned most matching persons. 5 by default; up to 10.  <br/>For example, if MaxFaceNum is 3 and MaxPersonNum is 5, up to 3*5 = 15 persons will be returned. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Results | Array of [Result](/document/api/867/32807#Result) | Recognition results. |
| FaceNum | Integer | Number of faces included in the groups searched in. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Sample 1. API for Face Search

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=SearchFaces
&Url=http://test.image.myqcloud.com/testA.jpg
&MaxFaceNum=1
&MinFaceSize=40
&MaxPersonNum=5
&GroupIds.0=TencentShenZhenEmployee
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Results": [
      {
        "Candidates": [
          {
            "PersonId": "1001",
            "FaceId": "2875093635484912302",
            "Score": 100
          }
        ],
        "FaceRect": {
          "X": 370,
          "Y": 46,
          "Width": 75,
          "Height": 75
        }
      }
    ],
    "FaceNum": 1,
    "RequestId": "57b42b73-b978-45b9-8095-8f50e9642d35"
  }
}
```

### Sample 2. Error

Error with image URL

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=SearchFaces
&Url=http://test.image.myqcloud.com/testA
&GroupIds.0=TencentShenZhenEmployee
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Error": {
      "Code": "FailedOperation.ImageDownloadError",
      "Message": "Error downloading the image."
    },
    "RequestId": "527ecffe-4c6a-47c9-8217-4dd2e3f018da"
  }
}
```

### Sample 3. Error

MaxFaceNum cannot be above 10

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=SearchFaces
&Url=http://test.image.myqcloud.com/testA.jpg
&MaxFaceNum=11
&GroupIds.0=TencentShenZhenEmployee
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Error": {
      "Code": "FailedOperation.SearchFacesExceed",
      "Message": "The number of faces searched exceeds the limit."
    },
    "RequestId": "f04ba2f3-532c-4207-9caa-6e818ded7fb9"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iai&Version=2018-03-01&Action=SearchFaces)

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

