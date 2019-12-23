
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
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. The difference between the timestamp and the server time cannot exceed 5 minutes. Check whether the local time is synced with the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature calculating error. Check the signature calculating process by referring to the documentation about API authentication in the calling method. |
| AuthFailure.TokenFailure | Invalid token. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used.  |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | API does not exist. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | A parameter is missing |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The request rate limit is exceeded |
| ResourceInUse | Resource is occupied. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource is unavailable |
| UnauthorizedOperation | Unauthorized operation |
| UnknownParameter | Unknown parameter |
| UnsupportedOperation | Unsupported operation |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |

### Service Error Codes



| Error Code | Description |
|:-------|:-----|
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InternalError.AccountUserNotAuthenticated | The account has not been authenticated. |
| InternalError.CidrConflictWithOtherCluster | The CIDR conflicts with a CIDR of another cluster. |
| InternalError.CidrConflictWithOtherRoute | The CIDR conflicts with another route. |
| InternalError.CidrConflictWithVpcCidr | The CIDR conflicts with the VPC. |
| InternalError.CidrConflictWithVpcGlobalRoute | The CIDR conflicts with the global route. |
| InternalError.CidrInvali | Invalid CIDR. |
| InternalError.CidrMaskSizeOutOfRange | Invalid CIDR mask. |
| InternalError.CreateMasterFailed | Cluster creation failed. |
| InternalError.CvmCommon | Error creating a node by CVM. |
| InternalError.Db | Database error. |
| InternalError.DbAffectivedRows | Database effective function error. |
| InternalError.InitMasterFailed | Master node initialization failed. |
| InternalError.InvalidPrivateNetworkCidr | Invalid CIDR. |
| InternalError.Param | Param. |
| InternalError.PublicClusterOpNotSupport | The cluster does not support the current operation. |
| InternalError.QuotaMaxClsLimit | Quota limit is exceeded. |
| InternalError.QuotaMaxNodLimit | Quota limit is exceeded. |
| InternalError.UnexceptedInternal | UnexceptedInternal. |
| InternalError.VpcCommon | VPC error. |
| InternalError.VpcRecodrNotFound | No VPC record found. |
| InvalidParameter | Invalid parameter. |
| LimitExceeded | Quota limit is exceeded. |
| ResourceNotFound | Resource does not exist. |
