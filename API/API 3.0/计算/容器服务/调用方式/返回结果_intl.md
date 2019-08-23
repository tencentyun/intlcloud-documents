## Response for Successful Requests

For example, when calling CVM API DescribeInstancesStatus (version 2017-03-12), if this request is successfully, the response is as followed:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response and its RequestId are common fields and are always returned as long as the API request is processed, regardless of whether the request is successful or not.
* `RequestId` is for identifying an API request. If an API exception occurs, please contact us with RequestId which helps locate the cause of the error.
* Any fields other than the common fields are API-specific fields. For more information on such fields, see the relevant API documentation. In this example, `TotalCount` and `InstanceStatusSet` are specific to the API DescribeInstancesStatus. Since the user who initiated the request does not have a CVM instance yet, 0 is returned for `TotalCount` and `InstanceStatusSet` is left empty.

## Response for Failed Requests

If the request fails, the response is as follows:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please ensure your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Error indicates request failure. Its two fields, Code and Message, will be returned in case of failure. 
* `Code` indicates the error code. When an error occurs with the request, you can use the error code to find the cause and solution for the error in the list of common error codes or API-specific error codes.
* `Message` describes the cause of the error. It may be updated without notice.
* `RequestId` is for identifying an API request. If an API exception occurs, please contact us with RequestId which helps locate the cause of the error.


## Common Error Codes


When you see the Error field in the response, it means that your request has failed; the Code field indicates the error code. The following are common error codes that all requests can return.


| Error Code | Description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. |
| AuthFailure.SignatureExpire | Signature expired |
| AuthFailure.SignatureFailure | Invalid signature. |
| AuthFailure.TokenFailure | Invalid token. |
| AuthFailure.UnauthorizedOperation | No CAM authorization |
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
