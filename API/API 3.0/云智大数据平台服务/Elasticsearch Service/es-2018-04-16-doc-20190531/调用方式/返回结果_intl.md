## Successful Response

For example, when calling the API DescribeInstancesStatus (version: 2017-03-12) to view the status of CVM instances, if the request has succeeded, you may see the response as shown below:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* The API will return `Response`, which contains `RequestId`, as long as it processes the request. It does not matter if the request is successful or not.
* RequestId is the unique ID of an API request. Contact us with this ID when an exception occurs.
* Except for the fixed fields, all fields are action-specified. For the definitions of action-specified fields, see the corresponding API documentation. In this example, `TotalCount` and `InstanceStatusSet `are the fields specified by the API `DescribeInstancesStatus`. As the requester does not have CVM instances yet, `TotalCount` is 0 and the `InstanceStatusSet` is empty.

## Error Response

If the call fails, you may see the response as shown below:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check if your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* In case of a failed request, Error, Code, and Message fields are returned.
* `Code` indicates the error code of the specific error. When the request goes wrong, you can use this error code to locate the cause and solution in the common error code list and the error code list corresponding to the current API.
* Message shows the specific cause of this error and it may change as Tencent Cloud services update.
* RequestId is the unique ID of an API request. Contact us with this ID when an exception occurs.


## Common Error Codes


If there is an Error field in the response, it means that the API call failed. The Code field in Error indicates the error code. The following table lists the common error codes that all actions can return.


| Error code | Error description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure. |
| AuthFailure.SecretIdNotFound | Key does not exist. |
| AuthFailure.SignatureExpire | Signature expired. |
| AuthFailure.SignatureFailure | Signature error. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | No CAM authorization. |
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
