
## Feature Description

If the Error field exists in the returned result, it means the API call failed. For example:

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

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common error codes

| Error Code | Description |
|--------|------|
| UnsupportedOperation | Unsupported operation. |
| ResourceInUse | Resource is occupied |
| InternalError | Internal error. |
| RequestLimitExceeded | The request rate limit is exceeded |
| AuthFailure.SecretIdNotFound | Key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| LimitExceeded | Quota limit is exceeded. |
| NoSuchVersion | The API version does not exist |
| ResourceNotFound | Resource does not exist |
| AuthFailure.SignatureFailure | Invalid signature. Signature calculation error. Please ensure that you have followed the signature calculation process as described in the API authentication documentation in the calling method. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time cannot differ by more than five minutes. Please ensure your current local time matches the standard time. |
| UnsupportedRegion | Unsupported region |
| UnauthorizedOperation | Unauthorized operation. |
| InvalidParameter | Incorrect parameter. |
| ResourceUnavailable | Resource is unavailable |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, please see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.TokenFailure | Invalid token |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| InvalidParameterValue | Invalid parameter value. |
| InvalidAction | API does not exist. |
| MissingParameter | A parameter is missing |
| ResourceInsufficient | Insufficient resource |


### Business error codes



| Error Code | Description |
|:-------|:-----|
| FailedOperation.CreateBucketFail | Failed to create the COS bucket. |
| InternalError.CmqError | An exception occurred during CMQ queue creation, probably because the CMQ queue to be created already exists, or your account has no permission or is in arrears. |
| InternalError.CreateAuditError | Error creating the tracking set. Please submit a ticket. |
| InternalError.DeleteAuditError | Failed to delete the tracking set. Please submit a ticket. |
| InternalError.DescribeAuditError | Error querying tracking set details. Please submit a ticket. |
| InternalError.InquireAuditCreditError | Error querying the maximum number of tracking sets that can be created. Please submit a ticket. |
| InternalError.ListAuditsError | Internal error querying the summary of tracking sets. Please submit a ticket. |
| InternalError.ListCmqEnableRegionError | Internal error. Please submit a ticket. |
| InternalError.ListCosEnableRegionError | Internal error. Please submit a ticket. |
| InternalError.SearchError | Internal error. Please submit a ticket. |
| InternalError.StartLoggingError | Internal error. Please submit a ticket. |
| InternalError.StopLoggingError | Internal error. Please submit a ticket. |
| InternalError.UpdateAuditError | Internal error. Please submit a ticket. |
| InvalidParameter.Time | The parameter must contain the start time and end time and must be an integer timestamp (accurate to the second). |
| InvalidParameterValue.AuditNameError | Tracking set name is non-compliant. |
| InvalidParameterValue.CmqRegionError | CloudAudit currently does not support the entered CMQ region. |
| InvalidParameterValue.CosNameError | The entered COS bucket name is non-compliant. |
| InvalidParameterValue.CosRegionError | CloudAudit currently does not support the entered COS region. |
| InvalidParameterValue.IsCreateNewBucketError | The value of IsCreateNewBucket can be 0 or 1. 0 represents not creating a bucket, while 1 creating a bucket. |
| InvalidParameterValue.IsCreateNewQueueError | The value of IsCreateNewQueue can be 0 or 1. 0 represents not creating a queue, while 1 creating a queue. |
| InvalidParameterValue.IsEnableCmqNotifyError | The value of IsEnableCmqNotify can be 0 or 1. 0 represents not enabling CMQ delivery, while 1 enabling. |
| InvalidParameterValue.LogFilePrefixError | Incorrect log prefix format. |
| InvalidParameterValue.MaxResult | The maximum number of entries returned by one search is 50. |
| InvalidParameterValue.QueueNameError | The entered queue name is non-compliant. |
| InvalidParameterValue.ReadWriteAttributeError | Valid values of the read/write attribute: 1 (read-only), 2 (write-only), 3 (read/write). |
| InvalidParameterValue.Time | The start time cannot be later than the end time. |
| InvalidParameterValue.attributeKey | Valid values of AttributeKey: RequestId, EventName, ReadOnly, Username, ResourceType, ResourceName, AccessKeyId. |
| LimitExceeded.OverAmount | The maximum number of tracking sets is exceeded. |
| LimitExceeded.OverTime | Only entries in the last 7 days can be searched for. |
| MissingParameter.MissAuditName | Tracking set name is missing. |
| MissingParameter.MissCosBucketName | COS bucket parameter is missing. |
| MissingParameter.MissCosRegion | COS region parameter is missing. |
| MissingParameter.cmq | If the value of IsEnableCmqNotify is 1, IsCreateNewQueue, CmqQueueName, and CmqRegion are required. |
| ResourceInUse.AlreadyExistsSameAudit | A tracking set with the same name already exists. |
| ResourceInUse.AlreadyExistsSameAuditCmqConfig | A tracking set with the same CMQ delivery configuration already exists. |
| ResourceInUse.AlreadyExistsSameAuditCosConfig | A tracking set with the same COS delivery configuration already exists. |
| ResourceInUse.CosBucketExists | The COS bucket already exists. |
| ResourceNotFound.AuditNotExist | The tracking set does not exist. |
