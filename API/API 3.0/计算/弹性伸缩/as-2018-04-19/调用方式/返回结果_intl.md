## Returned Result for Success

Take viewing the instance state list (DescribeInstancesStatus) version 2017-03-12 through the CVM API as an example. If the call succeeds, the possible returned result is as follows:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }
    
* `Response` and its internal `RequestId` are fixed fields and will be returned as long as request is processed by the API no matter whether the request succeeds.
* RequestId is the unique identifier of an API request. If an exception occurs, you can contact us and provide the ID for troubleshooting.
* Except for the fixed fields, all the fields are defined by the specific API. For the fields returned by different APIs, see the definitions in the API documentation. In this example, `TotalCount` and `InstanceStatusSet `are the fields defined by the `DescribeInstancesStatus` API. As the user who calls the request does not have a CVM instance yet, `TotalCount` returns a value of 0 in this case and the `InstanceStatusSet` list is empty.

## Return Result for Error

If the call fails, the returned result may look like the example below:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* The presence of the `Error` field indicates that the request call failed. The `Error` field and its `Code` and `Message` fields must be returned when the call fails.
* `Code` indicates the error code of the specific error. When the request goes wrong, you can use this error code to locate the cause and solution in the common error code list and the error code list corresponding to the current API.
* `Message` shows the specific cause of this error. The message text is subject to change or update from time to time by Tencent Cloud.
* RequestId is the unique identifier of an API request. If an exception occurs, you can contact us and provide the ID for troubleshooting.


## Common Error Codes


If there is an Error field in the returned result, it means that the API call failed. The Code field in Error indicates the error code. The error codes that may appear for all businesses are common error codes, which are listed below:


| Error code | Error description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | Key does not exist. |
| AuthFailure.SignatureExpire | Signature expired. |
| AuthFailure.SignatureFailure | Signature error. |
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
