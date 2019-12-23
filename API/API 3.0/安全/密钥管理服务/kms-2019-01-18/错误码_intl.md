
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

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure. |
| AuthFailure.SecretIdNotFound | Key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time cannot differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Invalid token. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | API does not exist. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | A parameter is missing. |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The request rate limit is exceeded. |
| ResourceInUse | Resource is occupied. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource is unavailable. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region. |

### Business Error Codes



| Error code | Description |
|:-------|:-----|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue.AliasAlreadyExists | The alias already exists. |
| InvalidParameterValue.DuplicatedKeyId | The KeyId is duplicated. |
| InvalidParameterValue.InvalidAlias | The alias is in incorrect format. |
| InvalidParameterValue.InvalidCiphertext | The ciphertext is in incorrect format. |
| InvalidParameterValue.InvalidKeyId | Invalid KeyId. |
| InvalidParameterValue.InvalidKeyUsage | Invalid KeyUsage. |
| InvalidParameterValue.InvalidPlaintext | Invalid plaintext. |
| InvalidParameterValue.InvalidType | Invalid type. |
| LimitExceeded.CmkLimitExceeded | The number of CMKs has reached the limit. |
| ResourceUnavailable.CmkDisabled | The CMK has been disabled. |
| ResourceUnavailable.CmkNotFound | The CMK does not exist. |
| UnauthorizedOperation | Unauthorized operation. |
