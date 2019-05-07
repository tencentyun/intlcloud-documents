## 1. API Description

API request domain name: iai.tencentcloudapi.com.

This API removes a person from a specified group. This action only affects the group. If the person exists only in the specified group, the person will be deleted, and all their face information will be deleted.

Default API request frequency limit: 50 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/867/32773).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DeletePersonFromGroup |
| Version | Yes | String | Common parameter; the value for this API: 2018-03-01 |
| Region | No | String | Common parameter; not passed in for this API |
| PersonId | Yes | String | Person ID |
| GroupId | Yes | String | Group ID |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Sample 1. API for Removing a Person from a Group

This API removes a person from a specified group. This action only affects the group

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=DeletePersonFromGroup
&PersonId=1001
&GroupId=TencentShenZhenEmployee
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "f9b22bbc-c94d-4287-a2ab-fa68f7bbbaf3"
  }
}
```

### Sample 2. Error

The specified person is not in the group

#### Input Sample Code

```
https://iai.tencentcloudapi.com/?Action=DeletePersonFromGroup
&PersonId=3001
&GroupId=ZhuYuanDormitoryNo1
&Version=2018-03-01
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Error": {
      "Code": "FailedOperation.GroupPersonMapNotExist",
      "Message": "The ID of the corresponding person is not in the group."
    },
    "RequestId": "b9d9641d-3de2-4a6f-a728-36a3b66e7bd0"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iai&Version=2018-03-01&Action=DeletePersonFromGroup)

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

