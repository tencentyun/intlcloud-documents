
## Feature Description

If there is an Error field in the returned result, it means that the API call failed. For example:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | Key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time must not differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Signature error. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | Request not authorized through CAM. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in. |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | API does not exist. |
| InvalidParameter | Parameter error. |
| InvalidParameterValue | Wrong parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | Parameter missing. |
| NoSuchVersion | API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the frequency limit. |
| ResourceInUse | Resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource not available. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | HTTP(S) request protocol error; only GET and POST requests are supported. |
| UnsupportedRegion | API does not support the passing region. |

### Business Error Codes

During the API call, successful calls and failed calls that return the error code InvalidParameterValue.NoFaceInPhoto (no face found in the image) are billable.

| Error Code | Description |
|:-------|:-----|
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

