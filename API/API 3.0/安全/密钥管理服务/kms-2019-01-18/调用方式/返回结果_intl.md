## Successful Response

Take viewing the instance state list (DescribeInstancesStatus) version 2017-03-12 through the CVM API as an example. If the call succeeds, the possible response is as follows:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* `Response` and its internal `RequestId` are fixed fields and will be returned as long as request is processed by the API no matter whether the request succeeds.
* RequestId is an unique ID for the API request. You can contact us with RequestId to troubleshoot issues. 
* Except for the fixed fields, all the fields are defined by the specific API. For the fields returned by different APIs, see the definitions in the API documentation. In this example, `TotalCount` and `InstanceStatusSet `are the fields defined by the `DescribeInstancesStatus` API. As the user who calls the request does not have a CVM instance yet, `TotalCount` returns a value of 0 in this case and the `InstanceStatusSet` list is empty.

## Error Response

If the call fails, the response may look like the example below:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* In case of a failed request, Error, Code, and Message fields are returned.
* `Code` indicates the error code of the specific error. When the request goes wrong, you can use this error code to locate the cause and solution in the common error code list and the error code list corresponding to the current API.
* Message shows the specific cause of this error. The message text is subject to change or update as the business develops or the experience gets optimized, so you should not rely on this return value.
* RequestId is an unique ID for the API request. You can contact us with RequestId to troubleshoot issues. 


## Common Error Codes


The Error field in the response indicates a failed API request, and the Code field indicates the error code. The following common error codes apply to all requests.


| Error code | Error description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure. |
| AuthFailure.SecretIdNotFound | Key does not exist. |
| AuthFailure.SignatureExpire | Signature expired. |
| AuthFailure.SignatureFailure | Signature error. |
| AuthFailure.TokenFailure | Invalid token. |
| AuthFailure.UnauthorizedOperation | No CAM authorization. |
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
