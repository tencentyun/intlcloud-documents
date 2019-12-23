
## Feature Description

If there is an Error field in the response, it means that the API call failed. For example:

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

Code in Error indicates the error code, and Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not a TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failed. |
| AuthFailure.SecretIdNotFound | Key does not exist. Check if the key has been deleted or disabled in the console, and if not, check if the key is correctly entered. Note that whitespaces should not exist before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time cannot differ by more than five minutes. Please ensure your current local time matches the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature calculation error. Please ensure you’ve followed the signature calculation process described in the Signature API documentation.  |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | The API does not exist. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value. |
| LimitExceeded | Quota limit exceeded. |
| MissingParameter | A parameter is missing. |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the frequency limit. |
| ResourceInUse | Resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | The resource does not exist. |
| ResourceUnavailable | Resource is unavailable. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | HTTP(S) request protocol error; only GET and POST requests are supported. |
| UnsupportedRegion | API does not support the requested region. |

### Service Error Codes



| Error Code | Description |
|:-------|:-----|
| FailedOperation.DisableDeleteMemberFromRootNode | Members cannot be deleted from the root. |
| FailedOperation.DisableQuitSelfCreatedOrganization | You cannot quit a Tencent Cloud Organization that you created. |
| FailedOperation.InOrganizationAlready | The account is already  in this Tencent Cloud Organization. |
| FailedOperation.MemberNameUsed | This name is already in use. |
| FailedOperation.NodeNotEmpty | There are members in this Tencent Cloud organizational unit. |
| FailedOperation.OrganizationExistAlready | The Tencent Cloud Organization already exists. |
| FailedOperation.OrganizationNotEmpty | There are members in this Tencent Cloud Organization. |
| FailedOperation.ReSentInvitation | The invitation has been sent before. |
| FailedOperation.SomeUinsNotInOrganization | Some UINs do not belong to the current organization. |
| FailedOperation.UserInOrganization | The account to be invited is already in a Tencent Cloud Organization. |
| FailedOperation.UserNotRegister | The account that sent the invitation is not a master account. |
| LimitExceeded.Members | Exceeded the maximum number of Tencent Cloud Organization members allowed. |
| LimitExceeded.NodeDepthExceedLimit | There are too many levels within this Tencent Cloud organizational unit. |
| LimitExceeded.NodeExceedLimit | Exceeded the maximum number of Tencent Cloud organizational units allowed. |
| ResourceInUse.NodeName | The organizational unit name is already in use. |
| ResourceInUse.NodeNameUsed | This name is already in use. |
| ResourceNotFound.InvitationNotExist | The invitation does not exist. |
| ResourceNotFound.MemberNotExist | The member does not exist. |
| ResourceNotFound.NodeNotExist | The Tencent Cloud organizational unit does not exist. |
| ResourceNotFound.OrganizationNotExist | The Tencent Cloud Organization does not exist. |
| ResourceNotFound.UserNotExist | The user does not exist. |
