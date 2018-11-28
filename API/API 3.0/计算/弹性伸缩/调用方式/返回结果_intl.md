## Successful Response

Take the CVM API "View Instance Status List" (DescribeInstancesStatus) (version 2017-03-12) as an example. If the call of this API is successful, the response is as follows:

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response and its RequestId are common fields and are always returned as long as the API request is processed, regardless of whether it is successful.
* RequestId is used to uniquely identify an API request. If an API exception occurs, you can contact us and provide this ID to solve the problem.
* Any fields other than the common fields are API-specific fields. For more information on such fields, see the relevant API documentation. In this example, TotalCount and InstanceStatusSet are specific to the API DescribeInstancesStatus. Since the user who initiated the request does not have a CVM instance yet, 0 is returned for TotalCount and InstanceStatusSet is left empty.

## Error Response

If the request fails, the response is as follows:

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* In case of a failed request, Error, Code and Message fields are returned.
* Code indicates the error code. When an error occurs with the request, you can use the error code to find the cause and solution for the error in the list of common error codes or API-specific error codes.
* Message indicates the cause for the error. It may be updated from time to time.
* RequestId is used to uniquely identify an API request. If an API exception occurs, you can contact us and provide this ID to solve the problem.


## Common Error Codes


The Error field in the response indicates a failed API request, and the Code field indicates the error code. The following common error codes apply to all requests.


| Error Code | Description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (it is not a cloud API key) |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist |
| AuthFailure.SignatureExpire | Signature expired |
| AuthFailure.SignatureFailure | Invalid signature |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.UnauthorizedOperation | Request has no CAM authorization |
| DryRunOperation | DryRun operation. It means that the request is successful, except that the DryRun parameter is passed additionally. |
| FailedOperation | Operation failed |
| InternalError | Internal error |
| InvalidAction | API does not exist |
| InvalidParameter | Invalid parameter |
| InvalidParameterValue | Invalid parameter value |
| LimitExceeded | Quota limit is exceeded |
| MissingParameter | A parameter is missing |
| NoSuchVersion | The API version does not exist |
| RequestLimitExceeded | The request rate limit is exceeded |
| ResourceInUse | Resource is in use |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist |
| ResourceUnavailable | Resource is unavailable |
| UnauthorizedOperation | Unauthorized operation |
| UnknownParameter | Unknown parameter |
| UnsupportedOperation | Unsupported operation |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |

