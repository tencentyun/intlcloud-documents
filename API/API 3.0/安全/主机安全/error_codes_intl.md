
## Feature Description

If the Error field exists in the returned result, it means the call to the API failed. For example:

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

### Common error codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (it is not a cloud API key) |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. The difference between the timestamp and the server time cannot exceed 5 minutes. Check whether the local time is synced with the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature computing error. Check the signature computing process by referring to the documentation about API authentication in the calling method. |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.UnauthorizedOperation | No CAM authorization |
| DryRunOperation | DryRun operation. It means that the request is successful, except that the DryRun parameter is passed additionally. |
| FailedOperation | Operation failed |
| InternalError | Internal error. |
| InvalidAction | API does not exist. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | A parameter is missing. |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The request rate limit is exceeded. |
| ResourceInUse | Resource is occupied. |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource is unavailable. |
| UnauthorizedOperation | Unauthorized operation |
| UnknownParameter | Unknown parameter |
| UnsupportedOperation | Unsupported operation |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |

### Service error codes

| Error Code | Description |
|:-------|:-----|
| FailedOperation.AgentOffline | The client is offline. |
| FailedOperation.CloseProVersion | Failed to deactivate HS Pro. |
| FailedOperation.CreateProcessTask | Failed to create a task to obtain real-time processes. |
| FailedOperation.InquiryPrice | Price query failed. |
| FailedOperation.MachineDelete | HS has been unmounted. |
| FailedOperation.PartSeparate | Some of the hosts failed to be isolated. |
| FailedOperation.PrePayMode | The HS Pro in the postpaid mode cannot be deactivated. |
| FailedOperation.ProcessTaskNotFound | The task to pull real-time processes does not exist. |
| FailedOperation.Recover | Failed to recover Trojans. |
| FailedOperation.RescanVul | Failed to redetect vulnerabilities. |
| FailedOperation.RescanVulProcessInUse | A redetection task is already in progress. |
| FailedOperation.SingleSeparate | Failed to isolate a single host. |
| FailedOperation.TradeError | Transaction error. |
| InternalError | Internal error. |
| InvalidParameter.DateRange | Invalid time range format. |
| InvalidParameter.IllegalRequest | Invalid request. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |
| InvalidParameter.MissingParameter | Missing parameter. |
| InvalidParameter.ParsingError | Parameter parsing error. |
| LimitExceeded.AreaQuota | The limit of batch addition is exceeded. |
| MissingParameter | A parameter is missing. |
| ResourceNotFound | Resource does not exist. |

