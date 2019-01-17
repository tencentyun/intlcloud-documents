
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

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not Cloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | Key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time must not differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Signature error. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | Request not authorized through CAM. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed. |
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
| FailedOperation.AsyncTaskAlreadyStarted | The task has already started. |
| FailedOperation.InvalidMsgLen | The message length is invalid. |
| FailedOperation.InvalidTopicName | The message topic is invalid. |
| FailedOperation.TaskIDNotMatch | User or product does not match the task ID. |
| FailedOperation.UpdateVersionNotMatch | The updated version does not match. |
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.DeviceAlreadyExist | Name of the created device already exists. |
| InvalidParameterValue.InvalidSQL | The SQL statement contains invalid characters. |
| InvalidParameterValue.JSONHasInvalidNode | The State JSON object contains invalid nodes. |
| InvalidParameterValue.JSONLevelExceedLimit | The number of layers of the State JSON object exceeds the limit; up to 6 layers are allowed. |
| InvalidParameterValue.JSONSizeExceedLimit | The size of the State JSON object exceeds the limit; up to 64 KB is allowed. |
| InvalidParameterValue.ParamIncomplete | Key field information missing in the request. |
| InvalidParameterValue.ProductAlreadyExist | Name of the created product already exists. |
| InvalidParameterValue.ProductTypeNotSupport | Product type is not supported. |
| InvalidParameterValue.TopicRuleAlreadyExist | The rule already exists. |
| LimitExceeded.DeviceExceedLimit | Number of devices exceeds the limit. |
| LimitExceeded.PengingOrProcessingTasksExceedLimit | Too many tasks in waiting and processing status. |
| LimitExceeded.ProductExceedLimit | Product quantity limit is exceeded. |
| ResourceNotFound.DeviceNotExist | Device does not exist. |
| ResourceNotFound.DeviceShadowNotExist | Device shadow does not exist. |
| ResourceNotFound.ProductNotExist | Product does not exist. |
| ResourceNotFound.ProductOrDeviceNotExist | This product or device does not exist for the user. |
| ResourceNotFound.TaskNotExist | Task does not exist. |
| UnauthorizedOperation.DeviceHasAlreadyBindGateway | This device is bound to a gateway device and cannot be deleted. |
| UnauthorizedOperation.DevicesExistUnderProduct | The product to be deleted contains devices that have not been deleted. |
| UnauthorizedOperation.GatewayHasBindedDevices | This device has devices bound to it. |
| UnauthorizedOperation.ProductCantHaveLoRaDevice | This product type cannot create LoRa devices. |
| UnauthorizedOperation.ProductCantHaveNotLoRaDevice | This product type can only create LoRa devices. |
| UnauthorizedOperation.ProductNotSupportPSK | The product does not support key-based authentication. |
| UnsupportedOperation.GatewayProductHasBindedProduct | The gateway product has sub-products bound to it and cannot be deleted. |
| UnsupportedOperation.ProductHasBindGateway | The current product has gateway devices bound to it and cannot be deleted. |
| UnsupportedOperation.ProductHasBindedGatewayProduct | The product has gateway products bound to it and cannot be deleted. |
