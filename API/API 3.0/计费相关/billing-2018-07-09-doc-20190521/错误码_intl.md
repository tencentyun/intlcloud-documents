
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
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure. |
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
| InvalidParameterValue | Wrong parameter value. |
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

### Business Error Codes



| Error code | Description |
|:-------|:-----|
| FailedOperation | Operation failed |
| FailedOperation.AgentPayDealCannotDown | Device paid by reseller cannot be degraded.. |
| FailedOperation.BalanceInsufficient | Insufficient account balance. |
| FailedOperation.InvalidDeal | Order status error. Only unpaid orders can be paid. |
| FailedOperation.InvalidVoucher | Voucher cannot be used. |
| FailedOperation.NeedPayTogeter | Orders purchased together must be paid at the same time. |
| FailedOperation.PayPriceError | Payment failed, contact Tencent Cloud staff to resolve this issue. |
| FailedOperation.PaySuccDeliverFailed | Payment was successful but delivery failed. Contact Tencent Cloud staff to resolve this issue.  |
| FailedOperation.SummaryDataNotReady | Summary is in compilation. Please try again later. |
| FailedOperation.TagKeyNotExist | The cost allocation tag key does not exist |
| InvalidParameter | Parameter error |
| InvalidParameterValue | Incorrect parameter value |
| UnauthorizedOperation.NotCertification | The account has not completed identity verification. Payment failed. |
| UnauthorizedOperation.NotFinanceAuth | The account has not been authorized for financial transactions. Payment failed. |
