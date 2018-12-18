## Common Error Codes
The error code in the response represents the result of the cloud API call. Here, "code" is a common error code that applies to the APIs of all modules. If "code" is 0, the call succeeded; otherwise, the call failed. If the call failed, you can determine the cause of the error and take appropriate action according to the table below.

<table class="t">
<tbody><tr>
<th> <b>Error code</b>
</th><th> <b>Error type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> 4000
</td><td> Invalid request parameter
</td><td> A required parameter is missing, or the parameter value is in wrong format. For the specific error information, see the message field in the error description.
</td></tr>
<tr>
<td> 4100
</td><td> Authentication failed
</td><td> Signature authentication failed. For more information, see the Authentication section in the documentation.
</td></tr>
<tr>
<td> 4200
</td><td> Request expired
</td><td> The request has expired. For more information, see the Request Validity section in the documentation.
</td></tr>
<tr>
<td> 4300
</td><td> Access denied
</td><td> The account is blocked or beyond the user scope of the targeted API.
</td></tr>
<tr>
<td> 4400
</td><td> Quota exceeded
</td><td> The number of requests exceeds the quota limit. For more information, see the Request Quota section in the documentation.
</td></tr>
<tr>
<td> 4500
</td><td> Replay attack
</td><td> The Nonce and Timestamp parameters of requests are used to ensure that each request is only executed once on the server, so the Nonce of the current request cannot be the same as that of the last request, and the Timestamp cannot differ from that of the Tencent server by more than 2 hours.
</td></tr>
<tr>
<td> 4600
</td><td> Unsupported protocol
</td><td> The protocol is not supported. For more information, see the documentation.
</td></tr>
<tr>
<td> 5000
</td><td> Resource does not exist
</td><td> The instance corresponding to the resource ID does not exist, the instance has been returned, or the resources of other users have been accessed.
</td></tr>
<tr>
<td> 5100
</td><td> Resource operation failed
</td><td> The operation on the resource failed. For detailed error information, see the message field in the error description. Please try again later or contact customer service for assistance.
</td></tr>
<tr>
<td> 5200
</td><td> Resource purchase failed
</td><td> Failed to purchase resources. The cause could be unsupported instance configuration or insufficient resources.
</td></tr>
<tr>
<td> 5300
</td><td> Resource purchase failed
</td><td> Failed to purchase resources due to insufficient balance.
</td></tr>
<tr>
<td> 5400
</td><td> Partially executed successfully
</td><td> The batch operation is partially executed successfully. For details, see the method return value.
</td></tr>
<tr>
<td> 5500
</td><td> User qualification review failed
</td><td> Failed to purchase resources due to user qualification review failure.
</td></tr>
<tr>
<td> 6000
</td><td> Internal server error
</td><td> An error occurred inside the server. Please try again later or contact customer service for assistance.
</td></tr>
<tr>
<td> 6100
</td><td> Unsupported by current version
</td><td> This API is not supported by this version or the API is in maintenance state. Note: When this error occurs, please make sure that the domain name of the API is correct. The domain name may vary for different modules.
</td></tr>
<tr>
<td> 6200
</td><td> API temporarily inaccessible
</td><td> The current API is out of service for maintenance. Please try again later.
</td></tr></tbody></table>

## Module Error Codes
The message field indicates an error related to the module.
Below is an example:
"message": "(100004) projectId is incorrect"
It consists of two parts: the content in the () is the module error code and the content after the () is the specific error description.
The error conditions that may occur vary for different modules. You can locate the error according to the specific error description.
