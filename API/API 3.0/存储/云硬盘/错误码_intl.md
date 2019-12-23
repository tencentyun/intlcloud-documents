
## Feature Description

If the Error field exists in the returned result, it means the API call failed. For example:

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

Code in the Error field indicates the error code, and Message indicates the error message.

## Error Codes

### Common Error Codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (it is not a cloud API key) |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. The difference between the timestamp and the server time cannot exceed 5 minutes. Check whether the local time is synced with the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature computing error. Check the signature computing process by referring to the documentation about API authentication in the calling method. |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the explanation of authentication in [CAM](https://intl.cloud.tencent.com/document/product/598). |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used.  |
| FailedOperation | Operation failed |
| InternalError | Internal error |
| InvalidAction | API does not exist |
| InvalidParameter | Incorrect parameter |
| InvalidParameterValue | Invalid parameter value |
| LimitExceeded | Quota limit is exceeded |
| MissingParameter | A parameter is missing |
| NoSuchVersion | The API version does not exist |
| RequestLimitExceeded | The request rate limit is exceeded |
| ResourceInUse | Resource is occupied |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist |
| ResourceUnavailable | Resource is unavailable |
| UnauthorizedOperation | Unauthorized operation |
| UnknownParameter | Unknown parameter |
| UnsupportedOperation | Unsupported operation |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |

### Service Error Codes



| Error Code | Description |
|:-------|:-----|
| AutoSnapshotPolicyOutOfQuota | The number of scheduled snapshot policies has reached the limit. |
| InsufficientRefundQuota | Number of returned cloud disks has reached the limit and no more cloud disks can be returned. |
| InsufficientSnapshotQuota | The snapshot quota is insufficient. |
| InternalError.ComponentError | The request failed because of a dependent component. Contact customer service to resolve the issue. |
| InternalError.FailQueryResource | Failed to query the resource. |
| InternalError.ResourceOpFailed | The operation performed on the resource failed. For the specific error information, please see the Message field in the error description. Try again later or contact the customer service for help. |
| InvalidAccount.InsufficientBalance | Insufficient account balance. |
| InvalidAutoSnapshotPolicyId.NotFound | The `AutoSnapshotPolicyId` that was entered does not exist. |
| InvalidDisk.AlreadyBound | The cloud disk is already bound to an scheduled snapshot policy. |
| InvalidDisk.Attached | The cloud disk has been mounted. |
| InvalidDisk.Busy | The cloud disk is busy. Try again later. |
| InvalidDisk.Expire | The cloud disk has expired. |
| InvalidDisk.NotPortable | Non-elastic cloud disks are not supported. |
| InvalidDisk.NotSupportRefund | The cloud disk cannot be returned. |
| InvalidDisk.NotSupportSnapshot | The cloud disk does not have the snapshot capability. |
| InvalidDisk.NotSupported | This operation is not supported for cloud disks. |
| InvalidDisk.RepeatRefund | The cloud disk has been returned and cannot be returned again. |
| InvalidDisk.SnapshotCreating | A snapshot is being created for the cloud disk. Try again later. |
| InvalidDisk.TypeError | Invalid cloud disk type |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidFilter | The specified Filter is not supported. |
| InvalidInstance.NotSupported | cloud disks cannot be mounted to the CVM. |
| InvalidInstanceId.NotFound | The `InstanceId` of the instance does not exist. |
| InvalidParameter | Invalid parameter |
| InvalidParameter.DiskConfigNotSupported | The configured cloud disk is not supported in the region. |
| InvalidParameter.DiskSizeNotMatch | The size of the cloud disk does not match the snapshot size. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.BindDiskLimitExceeded | The number of tags bound to the disk exceeds the limit. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| InvalidSnapshot.NotSupported | This operation is not supported for the snapshot. |
| InvalidSnapshotId.NotFound | The `SnapshotId` does not exist. |
| LimitExceeded.InstanceAttachedDisk | The number of disks mounted to the instance exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |
| ResourceBusy | The resource is busy. Try again later. |
| ResourceInsufficient | Insufficient resource |
| ResourceInsufficient.OverQuota | The quota is insufficient. |
| ResourceUnavailable.TooManyCreatingSnapshot | There are currently too many snapshots being created across the entire network. |
| TradeDealConflict | Order conflict. |
| UnauthorizedOperation | Unauthorized operation |
| UnsupportedOperation.DiskEncrypt | The disk is encrypted. |
| UnsupportedOperation.InstanceNotStopped | The instance the cloud disk is mounted to has not been shut down. |
| UnsupportedOperation.SnapshotHasBindedImage | This snapshot created a custom snapshot. First delete the corresponding image. |
| UnsupportedOperation.StateError | The current status of the resource does not support this operation. |
| ZoneNotMatch | The cloud disk and the instance are not in the same availability zone. |
