
## Feature Description

If the `Error` field exists in the returned result, it means that the API call failed. For example:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please ensure your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

`Code` in `Error` indicates the error code, while `Message` indicates the specific information of the error.

## Error Code List

### Common error codes

| Error Code | Description |
|--------|------|
| UnsupportedOperation | Unsupported operation. |
| ResourceInUse | The resource is in use. |
| InternalError | Internal error. |
| RequestLimitExceeded | The request rate limit is exceeded. |
| AuthFailure.SecretIdNotFound | The key does not exist. Please check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| LimitExceeded | The quota limit is exceeded. |
| NoSuchVersion | The API version does not exist. |
| ResourceNotFound | The resource does not exist. |
| AuthFailure.SignatureFailure | Invalid signature. The signature calculation is incorrect. Please make sure that you have followed the signature calculation steps as described in the signature algorithm document in the calling method. |
| AuthFailure.SignatureExpire | Signature expired. The timestamp and server time cannot differ by more than five minutes. Please make sure that your current local time matches the standard time. |
| UnsupportedRegion | Unsupported region. |
| UnauthorizedOperation | Unauthorized operation. |
| InvalidParameter | Incorrect parameter. |
| ResourceUnavailable | The resource is unavailable. |
| AuthFailure.MFAFailure | MFA failure. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, please see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.TokenFailure | Invalid token. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| InvalidParameterValue | Invalid parameter value. |
| InvalidAction | The API does not exist. |
| MissingParameter | A parameter is missing. |
| ResourceInsufficient | Insufficient resource. |


### Business error codes



| Error Code | Description |
|:-------|:-----|
| FailedOperation.CreateBucketFail | Failed to create the COS bucket. |
| InternalError.CmqError | An exception occurred while creating the CMQ queue, probably because the CMQ queue to be created already exists, or your account has no permission or is in arrears. |
| InternalError.CreateAuditError | An error occurred while creating the tracking set. Please submit a ticket for assistance. |
| InternalError.DeleteAuditError | Failed to delete the tracking set. Please submit a ticket for assistance. |
| InternalError.DescribeAuditError | An error occurred while querying tracking set details. Please submit a ticket for assistance. |
| InternalError.InquireAuditCreditError | An error occurred while querying the maximum number of tracking sets that can be created. Please submit a ticket for assistance. |
| InternalError.ListAuditsError | An internal error occurred while querying the summary of tracking sets. Please submit a ticket for assistance. |
| InternalError.ListCmqEnableRegionError | Internal error. Please submit a ticket for assistance. |
| InternalError.ListCosEnableRegionError | Internal error. Please submit a ticket for assistance. |
| InternalError.SearchError | Internal error. Please submit a ticket for assistance. |
| InternalError.StartLoggingError | Internal error. Please submit a ticket for assistance. |
| InternalError.StopLoggingError | Internal error. Please submit a ticket for assistance. |
| InternalError.UpdateAuditError | Internal error. Please submit a ticket for assistance. |
| InvalidParameter.Time | The parameter must contain the start time and end time and must be an integer timestamp (accurate down to the second). |
| InvalidParameterValue.AuditNameError | The tracking set name is non-compliant. |
| InvalidParameterValue.CmqRegionError | CloudAudit currently does not support the entered CMQ region. |
| InvalidParameterValue.CosNameError | The entered COS bucket name is non-compliant. |
| InvalidParameterValue.CosRegionError | CloudAudit currently does not support the entered COS region. |
| InvalidParameterValue.IsCreateNewBucketError | The value of `IsCreateNewBucket` can be 0 or 1. 0 indicates not to create a bucket, while 1 indicates to create a bucket. |
| InvalidParameterValue.IsCreateNewQueueError | The value of `IsCreateNewQueue` can be 0 or 1. 0 indicates not to create a queue, while 1 indicates to create a queue. |
| InvalidParameterValue.IsEnableCmqNotifyError | The value of `IsEnableCmqNotify` can be 0 or 1. 0 indicates not to enable CMQ delivery, while 1 indicates to enable CMQ delivery. |
| InvalidParameterValue.LogFilePrefixError | Incorrect log prefix format. |
| InvalidParameterValue.MaxResult | The maximum number of entries returned in one search is 50. |
| InvalidParameterValue.QueueNameError | The entered queue name is non-compliant. |
| InvalidParameterValue.ReadWriteAttributeError | Valid values of the read/write attribute: 1 (read-only), 2 (write-only), 3 (read/write). |
| InvalidParameterValue.Time | The start time cannot be after the end time. |
| InvalidParameterValue.attributeKey | Valid values of `AttributeKey`: RequestId, EventName, ReadOnly, Username, ResourceType, ResourceName, AccessKeyId. |
| LimitExceeded.OverAmount | The maximum number of tracking sets is exceeded. |
| LimitExceeded.OverTime | Only entries for the last 7 days can be searched for. |
| MissingParameter.MissAuditName | The tracking set name is missing. |
| MissingParameter.MissCosBucketName | The COS bucket parameter is missing. |
| MissingParameter.MissCosRegion | The COS region parameter is missing. |
| MissingParameter.cmq | If the value of `IsEnableCmqNotify` is 1, `IsCreateNewQueue`, `CmqQueueName`, and `CmqRegion` are required. |
| ResourceInUse.AlreadyExistsSameAudit | A tracking set with the same name already exists. |
| ResourceInUse.AlreadyExistsSameAuditCmqConfig | A tracking set with the same CMQ delivery configuration already exists. |
| ResourceInUse.AlreadyExistsSameAuditCosConfig | A tracking set with the same COS delivery configuration already exists. |
| ResourceInUse.CosBucketExists | The COS bucket already exists. |
| ResourceNotFound.AuditNotExist | The tracking set does not exist. |
