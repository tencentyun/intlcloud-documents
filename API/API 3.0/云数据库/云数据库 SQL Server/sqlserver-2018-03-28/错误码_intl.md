
## Feature Description

If the Error field exists in the returned result, it means the API call failed. For example:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please verify if your signature is correct."
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
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in. |
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
| FailedOperation.CreateOrderFailed | Failed to create the order. |
| FailedOperation.CreateOrderFailed | Failed to get VPC information. |
| FailedOperation.QueryOrderFailed | Failed to query the order. |
| FailedOperation.QueryPriceFailed | Billing error. Failed to query the price. |
| InternalError | Internal error. |
| InternalError.CreateFlowFailed | Failed to create the flow. |
| InternalError.DBError | Database error. |
| InternalError.GcsError | GCS API error. |
| InternalError.SystemError | System error. |
| InternalError.UnknownError | Unknown error. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameter.InputIllegal | Invalid input. |
| InvalidParameter.ParamsAssertFailed | Parameter assertion conversion error. |
| InvalidParameterValue.BadGoodsNum | Invalid number of purchased instances. |
| InvalidParameterValue.IllegalRegion | Invalid region. |
| InvalidParameterValue.IllegalSpec | Invalid instance specification information. |
| InvalidParameterValue.IllegalZone | Invalid AZ ID. |
| InvalidParameterValue.InstanceExpandVolumeLow | The expansion capacity of the instance is lower than the current capacity. |
| InvalidParameterValue.ParameterTypeError | Incorrect parameter type. |
| ResourceNotFound.AccountNotExist | The account does not exist. |
| ResourceNotFound.DBNotFound | The database does not exist. |
| ResourceNotFound.InstanceNotFound | The instance does not exist. |
| ResourceNotFound.VpcNotExist | The VPC does not exist. |
| ResourceUnavailable.AccountInvalidStatus | Invalid account status. |
| ResourceUnavailable.InstanceMigrateRegionIllegal | Invalid instance migration region. |
| ResourceUnavailable.InstanceMigrateStatusInvalid | Invalid instance migration status. |
| ResourceUnavailable.InstanceStatusInvalid | Invalid instance status. |
