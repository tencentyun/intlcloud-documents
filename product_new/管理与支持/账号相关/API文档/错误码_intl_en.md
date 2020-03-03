## Feature Description
If an API call fails, you can reference the error code to check the error information.
- **`code`** is a common error code applicable to all APIs. If `code` is 0, the call succeeded; otherwise, the call failed, and you can determine the cause of the error and take corresponding actions based on the list of common error codes.
- **`message`** describes the error.
Each error consists of two parts: the content in the `()` is the error code, and the content after the `()` is the specific error description. You can determine the cause of the error and take corresponding actions based on the error code list.

Sample:
```shell
{
    "code": 5100,
    "message": "(100004) incorrect projectId"
}
```

## Error Codes
### Common errors

<table class="t">
<tbody><tr>
<th> <b>Error Code</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> 4000
</td><td> Invalid request parameter
</td><td> A required parameter is missing, or the parameter value is incorrectly formatted. For detailed error information, please see the `message` field.
</td></tr>
<tr>
<td> 4100
</td><td> Authentication failed
</td><td> Signature authentication failed. For more information, please see the Authentication section in the documentation.
</td></tr>
<tr>
<td> 4200
</td><td> Request expired
</td><td> The request has expired. For more information, please see the Request Validity Period section in the documentation.
</td></tr>
<tr>
<td> 4300
</td><td> Access denied
</td><td> The account is blocked or not authorized to use the API.
</td></tr>
<tr>
<td> 4400
</td><td> Quota exceeded
</td><td> The number of requests exceeds the quota limit. Please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.
</td></tr>
<tr>
<td> 4500
</td><td> Replay attack
</td><td> The `Nonce` and `Timestamp` parameters ensure that each request will be executed only once on the server. The `Nonce` parameter must be unique, and the difference between `Timestamp` and Tencent server time should not be greater than 2 hours.
</td></tr>
<tr>
<td> 4600
</td><td> Unsupported protocol
</td><td> The protocol is not supported. For more information, please see the documentation.
</td></tr>
<tr>
<td> 5000
</td><td> The resource does not exist
</td><td> The instance corresponding to the resource ID does not exist, the instance has been returned, or resource accessed belongs to other users.
</td></tr>
<tr>
<td> 5100
</td><td> Resource operation failed
</td><td> The operation on the resource failed. For detailed error information, please see the `message` field. Please try again later or <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.
</td></tr>
<tr>
<td> 5200
</td><td> Resource purchase failed
</td><td> Failed to purchase the resource. Possible causes include unsupported instance configuration or insufficient resources.
</td></tr>
<tr>
<td> 5300
</td><td> Resource purchase failed
</td><td> Failed to purchase the resource due to insufficient balance.
</td></tr>
<tr>
<td> 5400
</td><td> Partially executed
</td><td> A part of the batch operation has been performed successfully. For more information, please see the returned value of the method.
</td></tr>
<tr>
<td> 5500
</td><td> User qualification review failed
</td><td> Failed to purchase the resource due to user qualification review failure.
</td></tr>
<tr>
<td> 6000
</td><td> Internal server error
</td><td> An error occurred inside the server. Please try again later or <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for assistance.
</td></tr>
<tr>
<td> 6100
</td><td> Unsupported by current version
</td><td> The API is not supported by the current version or is under maintenance. Note: when this error occurs, please first check whether the domain name of the API is correct, as the domain name may vary by module.
</td></tr>
<tr>
<td> 6200
</td><td> API temporarily inaccessible
</td><td> The current API is under maintenance and not in service. Please try again later.
</td></tr><tr>
<td> 100193
</td><td> Payment failed
</td><td> Orders in the same purchase should be paid for together.
</td></tr></tbody></table>

### Action-specific errors
#### Error codes for project creation, deletion, and update

| Error Code | Description | Solution |
| ------ | -------------------------- | ---------------------------- |
| 1000   | The record does not exist                 | -                            |
| 1006   | The `APPID` does not exist                | Please check whether the `APPID` is correctly entered.    |
| 1007   | Invalid user                   | Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. |
| 1015   | The maximum limit of user-created projects has been reached | Exceeds the maximum limit of 500.            |
| 1036   | The project name already exists           | Please change the project name.               |
| 1072   | Unavailable project                 | The project has been disabled. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.            |
| 9003 | No project name               | Please enter a project name.               |

#### Error codes for project query
| Error Code | Description | Solution |
| ------ | -------------------------- | ---------------------------- |
| 9003   | Incorrect query parameter               |-                              |
| 1000   | No project ID                 |-                              |



