
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

| Error code | Description |
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
| InternalError | Internal error |
| InvalidAction | API does not exist. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | Parameter missing. |
| NoSuchVersion | API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the rate limit. |
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



| Error code | Description |
|:-------|:-----|
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| FailedOperation.UnSupportError | The instance does not support this API. |
| FailedOperation.Unknown | Invalid data is entered for weekday. |
| InternalError.DbOperationFailed | Internal system error with the DB operation, which may be update, insert, select, etc. |
| InternalError.InternalError | Internal error. |
| InvalidParameter | Parameter error |
| InvalidParameter.EmptyParam | Parameter is empty. |
| InvalidParameter.InvalidParameter | Business parameter error. |
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
| LimitExceeded.InvalidMemSize | The requested capacity is not in the capacity specifications (memSize should be an integral multiple of 1,024 in MB). |
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
