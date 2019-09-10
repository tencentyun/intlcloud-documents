## Successful Response

For example, when calling CVM API (version: 2017-03-12) to view the status of instances (DescribeInstancesStatus), if the request has succeeded, you may see the response as shown below:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* The API will return `Response`, which contains `RequestId`, as long as it processes the request. It does not matter if the request is successful or not.
* `RequestId` is the unique ID of an API request. Contact us with this ID when an exception occurs.
* Any fields other than the common fields are API-specific fields. For more information on such fields, see the relevant API documentation. In this example, TotalCount and InstanceStatusSet are specific to the API DescribeInstancesStatus. Since the user who initiated the request does not have a CVM instance yet, 0 is returned for TotalCount and InstanceStatusSet is left empty.

## Error Response

If the call has failed, you may see the response as shown below:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please ensure your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* In case of a failed request, Error, Code and Message fields are returned.
* `Code` is the code of the error that helps you identify the cause and solution. There are two types of error codes so you may find the code in either common error codes or API-specified error codes.
* `Message` describes the cause of this error and it may change as Tencent Cloud services update.
* RequestId is the unique ID of an API request. Contact us with this ID when an exception occurs.


## Common Error Codes


The Error field in the response indicates a failed API request, and the Code field indicates the error code. The following common error codes apply to all requests.


| Error code | Error description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. |
| AuthFailure.SignatureExpire | Signature expired |
| AuthFailure.SignatureFailure | Invalid signature |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.UnauthorizedOperation | No CAM authorization |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed |
| InternalError | Internal error |
| InvalidAction | API does not exist. |
| InvalidParameter | Incorrect parameter |
| InvalidParameterValue | Invalid parameter value |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | A parameter is missing |
| NoSuchVersion | The API version does not exist |
| RequestLimitExceeded | The request rate limit is exceeded |
| ResourceInUse | Resource is occupied |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist |
| ResourceUnavailable | Resource is unavailable |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |
