
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
| AuthFailure.InvalidSecretId | Invalid key (not Cloud API key type). |
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
| InvalidParameterValue | Incorrect parameter value. |
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



| Error code | Description |
|:-------|:-----|
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in |
| FailedOperation | Operation failed |
| FailedOperation.InvokeVideoApiFail | An exception occurred when operation the VOD API. |
| InternalError | Internal error |
| InternalError.ArgsNotMatch | For the API that is used for adding transcoding template |
| InternalError.CallOtherSvrError | Error calling internal service. |
| InternalError.ConfInUsed | The template is in use. |
| InternalError.ConfNotFound | The template does not exist. |
| InternalError.ConfOutLimit | The number of templates exceeds the display. |
| InternalError.ConfigNotExist | The configuration does not exist. |
| InternalError.ConnectDbError | DB connection error. |
| InternalError.CrtDateInUsing | The certificate is in use. |
| InternalError.CrtDateNotFound | The certificate does not exist. |
| InternalError.CrtDateNotLegal | The certificate is invalid. |
| InternalError.CrtDateOverdue | The certificate has expired. |
| InternalError.CrtDomainNotFound | There is no related domain name. |
| InternalError.CrtKeyNotMatch | The certificate key does not match. |
| InternalError.DBError | DB execution error. |
| InternalError.GetBizidError | Error getting user account. |
| InternalError.GetStreamInfoError | Failed to get stream information. |
| InternalError.GetUpstreamInfoError | Error getting live stream source information. |
| InternalError.GetWatermarkError | Error getting the watermark. |
| InternalError.InvalidInput | Parameter check failed. |
| InternalError.InvalidUser | Account information error. |
| InternalError.NotFound | The record does not exist. |
| InternalError.NotPermmitOperat | No permission to operate. |
| InternalError.PlayDomainNoRecord | The playback domain name does not exist. |
| InternalError.ProcessorAlreadyExist | The transcoding template name already exists. |
| InternalError.PushDomainNoRecord | The push domain name does not exist. |
| InternalError.RuleAlreadyExist | The rule has already been configured. |
| InternalError.RuleInUsing | The rule is in use. |
| InternalError.RuleNotFound | The rule does not exist. |
| InternalError.RuleOutLimit | The rule exceeds the limit. |
| InternalError.StreamStatusError | Exceptional stream status. |
| InternalError.SystemError | Internal system error. |
| InternalError.UpdateDataError | Failed to update data. |
| InternalError.WatermarkEditError | Internal error modifying the watermark. |
| InternalError.WatermarkNotExist | The watermark does not exist. |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| LimitExceeded | Quota limit is exceeded |
| MissingParameter | Missing parameter |
| ResourceInUse | Resource is in use |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist |
| ResourceNotFound.TaskId | TaskId does not exist |
| ResourceUnavailable | Resource not available |
| UnauthorizedOperation | Unauthorized operation |
| UnknownParameter | Unknown parameter error |
| UnsupportedOperation | Unsupported operation |

