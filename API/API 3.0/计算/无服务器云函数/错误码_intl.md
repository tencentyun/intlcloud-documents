
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
| InvalidParameterValue | Wrong parameter value. |
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
| InternalError | Internal error |
| InternalError.System | Internal system error. |
| InvalidParameterValue | An invalid value was declared for the input parameter. |
| InvalidParameterValue.Cdn | An invalid value was declared for the input parameter: CDN. |
| InvalidParameterValue.Ckafka | An invalid value was declared for the input parameter: Ckafka. |
| InvalidParameterValue.Cmq | An invalid value was declared for the input parameter: CMQ. |
| InvalidParameterValue.Code | An invalid value was declared for the input parameter: Code. |
| InvalidParameterValue.Cos | An invalid value was declared for the input parameter: COS. |
| InvalidParameterValue.DateTime | An invalid value was declared for the input parameter: DateTime |
| InvalidParameterValue.Description | An invalid value was declared for the input parameter: Description |
| InvalidParameterValue.Environment | An invalid value was declared for the input parameter: Environment |
| InvalidParameterValue.FunctionName | An invalid value was declared for the input parameter: FunctionName |
| InvalidParameterValue.Handler | An invalid value was declared for the input parameter: Handler |
| InvalidParameterValue.Order | An invalid value was declared for the input parameter: Order |
| InvalidParameterValue.Orderby |An invalid value was declared for the input parameter: Orderby |
| InvalidParameterValue.Param | The input parameter is not in standard JSON format. |
| InvalidParameterValue.Runtime | An invalid value was declared for the input parameter: Runtime |
| InvalidParameterValue.TriggerDesc | An invalid value was declared for the input parameter: TriggerDesc. |
| InvalidParameterValue.TriggerName | An invalid value was declared for the input parameter: TriggerName. |
| InvalidParameterValue.Type | An invalid value was declared for the input parameter: Type. |
| LimitExceeded.Cdn | CDN usage exceeds the upper limit. |
| LimitExceeded.Function | The number of functions exceeds the upper limit. |
| LimitExceeded.FunctionOnTopic | The number of functions under the same topic exceeds the upper limit. |
| LimitExceeded.Memory | Memory exceeds the upper limit. |
| LimitExceeded.Offset | Offset is out of range. |
| LimitExceeded.Timeout | Timeout exceeds the upper limit. |
| LimitExceeded.Trigger | The number of triggers exceeds the upper limit. |
| MissingParameter.Code | Code parameter missing. |
| ResourceInUse.Cdn | CDN is in use. |
| ResourceInUse.Cmq | CMQ is in use. |
| ResourceInUse.Cos | COS is in use. |
| ResourceInUse.FunctionName | FunctionName already exists. |
| ResourceNotFound.Cdn | CDN does not exist. |
| ResourceNotFound.Ckafka | CKafka does not exist. |
| ResourceNotFound.Cmq | CMQ does not exist. |
| ResourceNotFound.Cos | COS does not exist. |
| ResourceNotFound.FunctionName | Function does not exist. |
| ResourceNotFound.FunctionVersion | Function version does not exist. |
| ResourceUnavailable.InsufficientBalance | The balance is insufficient. Please top up first. |
| UnauthorizedOperation | Unauthorized operation |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnauthorizedOperation.Region | Error with Region. |
| UnsupportedOperation.Cdn | CDN is not supported. |
| UnsupportedOperation.Cos | COS operation is not supported. |
| UnsupportedOperation.Trigger | Trigger operation is not supported. |

