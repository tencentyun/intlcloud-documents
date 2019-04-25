## API Responses for Success Requests

Example: this example describes the status of the specified instance (DescribeInstancesStatus) with version 2017-03-12. Below is a sample respond indicating the success of an API call.
    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* The API tells clients whether the request worked as expected by sending a response contains a RequestId parameter.
* RequestId is the ID of an API request. The RequestId is required to troubleshoot issues.
* Except for the fixed fields, all the fields are defined by the specific API. For the fields returned by different APIs, see the definitions in the API documentation. In this example, TotalCount and InstanceStatusSet are the fields defined by the DescribeInstancesStatus API. As the user who calls the request does not have a Cloud Virtual Machine instance yet, TotalCount returns a value of 0 in this case and the InstanceStatusSet list is empty.

##  API Responses for Errors

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

* Errors indicates that the call may failed.
The API returns Error, which contains Code and Message, when the request went wrong.
* Code is the unique error response code, which is returned when an API request fails and indicates the details of the error, and helps identify why the errors occur and how to solve them.
* Message explains the cause of the error. Note that the returned messages are subject to change. The information the messages provided may not be up-to-date. So please not use it as your only and primary reference.
* RequestId is the ID of an API request. The RequestId is required to troubleshoot issues.


## Common Error Codes


Errors indicates that the call may failed. The Code field in Error indicates the error code. The Code field in Error indicates the error code. The following error codes are common to all errors:



| Error code | Error description |
|----------|----------|
| AuthFailure.InvalidSecretId | Invalid key (not Cloud API key type). |
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
| InvalidParameterValue | Incorrect parameter value. |
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

