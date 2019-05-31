
## Feature Description

When an API call fails, an *Error* is returned in the result. For example:

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

In *Error*, *Code* indicates the error code, and *Message* specifies the detailed information of that error.

## Error Code List

### Common Error Codes

| Error code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | The provided SecretId could not be validated (the type of the SecretId may not be authorized by TencentCloud API). |
| AuthFailure.MFAFailure | Multi-factor authentication (MFA) error. |
| AuthFailure.SecretIdNotFound | The provided SecretId could not be found. The key may have been deleted or disabled in the console, or you may have entered the SecretId correctly, where no leading or trailing spaces are allowed.|
| AuthFailure.SignatureExpire | The Signature has expired. The difference between Timestamp and server time needs to be no larger than five minutes. Please ensure your local time matches the standard time. |
| AuthFailure.SignatureFailure | The Signature was not calculated correctly. Please follow the API authentication documentation to calculate the signature. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | CAM did not authorize this request. |
| DryRunOperation | DryRun operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | The operation failed. |
| InternalError | The error is caused internally. |
| InvalidAction | The API or action requested is not valid. |
| InvalidParameter | A parameter is not valid or cannot be used for the request.  |
| InvalidParameterValue | A value specified in a parameter is not valid or cannot be used for this request. |
| LimitExceeded | The upper limit of the quota limit is exceeded. |
| MissingParameter | A required parameter is missing for the request. |
| NoSuchVersion | The specified API version does not exist or is not found. |
| RequestLimitExceeded | The number of requests exceeds the rate limit. |
| ResourceInUse | The specified resource is occupied. |
| ResourceInsufficient | The specified resource is insufficient for the request. |
| ResourceNotFound | The specified resource does not exist or is not found. |
| ResourceUnavailable | The specified resource is not available. |
| UnauthorizedOperation | The operation is unauthorized. |
| UnknownParameter | An unknown parameter was specified in the request. |
| UnsupportedOperation | The operation is unsupported. |
| UnsupportedMethod| The HTTP(S) method used for the request is not supported; only GET and POST  are supported. Only GET and POST method are supported in HTTP protocol. |
| UnsupportedRegion | The API does not recognize or support the region where the request was sent. |

### Application Error Codes



| Error code | Description |
|:-------|:-----|
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| FailedOperation.UnSupportError | The instance does not support this API. |
| FailedOperation.Unknown | Invalid data is entered for weekday. |
| InternalError.DbOperationFailed | Internal database operation (e.g., update, insert, or select) errors. |
| InternalError.InternalError | Internal error. |
| InvalidParameter | Parameter error |
| InvalidParameter.EmptyParam | The specified parameter is not allowed to have an empty value. |
| InvalidParameter.InvalidParameter | Application parameter error. |
| InvalidParameter.OnlyVPCOnSpecZoneId | Only VPCs are provided in Shanghai financial availability zone. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |
| InvalidParameterValue.BackupNotExists | The backup does not exist. |
| InvalidParameterValue.InvalidInstanceTypeId | Error with the type of instances requested for purchase (TypeId - 1: cluster edition; 2: master-slave edition, i.e., the legacy master-slave edition). |
| InvalidParameterValue.InvalidSubnetId | In a VPC, vpcid or subnet ID is invalid. |
| InvalidParameterValue.MemSizeNotInRange | The requested capacity is out of the purchasable capacity range. |
| InvalidParameterValue.PasswordEmpty | Password is empty. |
| InvalidParameterValue.PasswordError | Wrong password. |
| InvalidParameterValue.PasswordRuleError | When the password is set, the old password passed in by MC does not match the previously set password. |
| InvalidParameterValue.ReduceCapacityNotAllowed | The request capacity is too small. Capacity reduction is not supported. |
| InvalidParameterValue.UnSupportedType | The instance type is not supported. |
| InvalidParameterValue.WeekDaysIsInvalid | Invalid data is entered for weekday. |
| ResourceUnavailable.AccountBalanceNotEnough | The order number of the request does not exist. |
| LimitExceeded.InvalidParameterGoodsNumNotInRange | The number of instances requested for purchase at a time is out of the purchasable quantity range. |
| LimitExceeded.PeriodExceedMaxLimit | The requested length of purchase is more than 3 years and exceeds the maximum value. |
| LimitExceeded.PeriodLessThanMinLimit | The length of purchase is invalid. It must be at least one month. |
| ResourceInUse.InstanceBeenLocked | The instance is locked by another process. |
| ResourceNotFound.AccountDoesNotExists | The uin value is blank. |
| ResourceNotFound.InstanceNotExists | No Redis instance found by the serialId. |
| ResourceUnavailable.AccountBalanceNotEnough | The request order number does not exist. |
| ResourceUnavailable.BackupLockedError | The backup has been locked by another task, and the action cannot be performed temporarily. |
| ResourceUnavailable.BackupStatusAbnormal | Exception with the backup status. The action cannot be performed temporarily. The backup may have expired or been deleted. |
| ResourceUnavailable.CallOssError | Failed to call the backend API. |
| ResourceUnavailable.GetSecurityError | Failed to get the security group information. |
| ResourceUnavailable.InstanceConfError | Error with the instance configuration. |
| ResourceUnavailable.InstanceDeleted | The instance has already been reclaimed. |
| ResourceUnavailable.InstanceLockedError | Redis has been locked by another process. |
| ResourceUnavailable.InstanceStateError | Error with the instance status. |
| ResourceUnavailable.InstanceStatusAbnormal | The Redis status is exceptional, and the corresponding process cannot be executed. |
| ResourceUnavailable.NoEnoughVipInVPC | Insufficient IP resources in the VPC. |
| ResourceUnavailable.NoRedisService | The requested region currently does not provide the requested type of Redis service. |
| ResourceUnavailable.NoTypeIdRedisService | The requested region currently does not provide the requested type of Redis service. |
| ResourceUnavailable.SecurityGroupNotSupported | The product has not accessed any security group. |
| UnauthorizedOperation | Unauthorized operation. |
| UnauthorizedOperation.NoCAMAuthed | No CAM permissions. |
| UnauthorizedOperation.UserNotInWhiteList | User is not in the whitelist. |
| UnsupportedOperation.ClusterInstanceAccessedDeny | The Redis cluster edition is not allowed to access a security group. |
| UnsupportedOperation.IsAutoRenewError | Error with the auto-renewal flag. |
| UnsupportedOperation.OnlyClusterInstanceCanExportBackup | Only cluster edition instances support backup exporting. |
