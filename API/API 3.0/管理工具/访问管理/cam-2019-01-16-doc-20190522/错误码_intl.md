
## Feature Description

If there is an Error field in the response, it means that the API call failed. For example:

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

Code in Error indicates the error code, and Message indicates the cause of the error.

## Error Code List

### Common Error Codes

| Error code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | The key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time must not differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Signature error. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | Request not authorized through CAM. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in. |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | The API does not exist. |
| InvalidParameter | Parameter error. |
| InvalidParameterValue | Wrong parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | Parameter missing. |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the frequency limit. |
| ResourceInUse | Resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | The resource does not exist. |
| ResourceUnavailable | Resource not available. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | HTTP(S) request protocol error; only GET and POST requests are supported. |
| UnsupportedRegion | API does not support the requested region. |

### Business Error Codes



| Error code | Description |
|:-------|:-----|
| FailedOperation.PolicyFull | The number of user policies exceeds the upper limit. |
| FailedOperation.PolicyNameInUse | The policy name specified by the PolicyName field already exists. |
| InternalError.SystemError | Internal error. |
| InvalidParameter.ActionError | The Action field of the policy document is invalid. |
| InvalidParameter.AttachmentFull | The number of policies associated with the authorization object of the principal field has reached the upper limit. |
| InvalidParameter.ConditionError | The condition field of the policy document is invalid. |
| InvalidParameter.DescriptionLengthOverlimit | The input parameter Description cannot exceed 300 bytes in length. |
| InvalidParameter.EffectError | The Effect field of the policy document is invalid. |
| InvalidParameter.EntityFilterError | The EntityFilter field is invalid. |
| InvalidParameter.GroupFull | The number of user groups has reached the upper limit. |
| InvalidParameter.GroupIdError | The GroupId field is invalid. |
| InvalidParameter.GroupNameInUse | The name of the user group already exists. |
| InvalidParameter.GroupNotExist | The user group does not exist. |
| InvalidParameter.GroupUserFull | The number of sub-users in the user group has reached the upper limit. |
| InvalidParameter.IdentityNameInUse | The name of the identity provider already exists. |
| InvalidParameter.KeywordError | The Keyword field is invalid. |
| InvalidParameter.NotSupportProduct | CAM does not support the resource type specified in the policy document. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.PolicyDocumentError | The PolicyDocument field is invalid. |
| InvalidParameter.PolicyDocumentLengthOverLimit | The PolicyDocument field exceeds the length limit. |
| InvalidParameter.PolicyIdError | The input parameter PolicyId is invalid. |
| InvalidParameter.PolicyIdNotExist | The policy ID does not exist. |
| InvalidParameter.PolicyNameError | The PolicyName field is invalid. |
| InvalidParameter.PrincipalError | The principal field of the policy document is invalid. |
| InvalidParameter.ResourceError | The Resource field of the policy document is invalid. |
| InvalidParameter.ScopeError | The Scope field is invalid. |
| InvalidParameter.ServiceTypeError | The ServiceType field is invalid. |
| InvalidParameter.StatementError | The Statement field of the policy document is invalid. |
| InvalidParameter.SubUserFull | The number of sub-accounts has reached the upper limit. |
| InvalidParameter.SubUserNameInUse | The name of the sub-user already exists. |
| InvalidParameter.UinError | The Uin field is invalid. |
| InvalidParameter.UserGroupFull | The number of user groups to which the sub-user is added has reached the upper limit. |
| InvalidParameter.UserNotExist | The authorization object of the principal field does not exist. |
| InvalidParameter.VersionError | The Version field of the policy document is invalid. |
| InvalidParameterValue.MetadataError | Error with the metadata document of the identity provider. |
| InvalidParameterValue.NameError | Error with the name of the identity provider. |
| LimitExceeded.IdentityFull | The number of identity providers has reached the upper limit. |
| ResourceNotFound.GroupNotExist | The user group does not exist. |
| ResourceNotFound.IdentityNotExist | The identity provider does not exist. |
| ResourceNotFound.NotFound | The resource does not exist. |
| ResourceNotFound.PolicyIdNotFound | The resource specified by PolicyId does not exist. |
| ResourceNotFound.UserNotExist | The user does not exist. |
