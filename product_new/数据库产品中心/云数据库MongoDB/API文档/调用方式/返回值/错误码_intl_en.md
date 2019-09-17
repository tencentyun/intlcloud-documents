The `code` (error code) in the response body summarizes the result of the call and execution of a TencentCloud API.
Any code other than 0 indicates that the request was not properly executed. The `message` (error message) describes the error in detail. You can determine the API execution result based on the error code.
On some terminals (such as browsers), error messages in Chinese will be displayed in Unicode and need to be decoded.

**The following error codes may be returned by a TencentCloud API:**
<table class="t">
<tbody><tr>
<th> <b>Error Code</b>
</th><th> <b>Type</b>
</th><th> <b>Description</b>
</th></tr>
<tr>
<td> 4000
</td><td> Invalid request parameter
</td><td> A required parameter is missing, or the parameter value is incorrectly formatted. For detailed error information, see the `message` field.
</td></tr>
<tr>
<td> 4100
</td><td> Authentication failed
</td><td> Signature authentication failed. For more information, see the Authentication section in the documentation.
</td></tr>
<tr>
<td> 4200
</td><td> Request expired
</td><td> The request has expired. For more information, see the Request Validity Period section in the documentation.
</td></tr>
<tr>
<td> 4300
</td><td> Access denied
</td><td> The account is blocked or not authorized to use the API.
</td></tr>
<tr>
<td> 4400
</td><td> Quota exceeded
</td><td> The number of requests exceeds the quota limit. For more information, see the Request Quota section in the documentation.
</td></tr>
<tr>
<td> 4500
</td><td> Replay attack
</td><td> The `Nonce` and `Timestamp` parameters ensure that each request will be executed only once on the server. The `Nonce` parameter must be unique, and the difference between `Timestamp` and Tencent server time should not be greater than 2 hours.
</td></tr>
<tr>
<td> 4600
</td><td> Unsupported protocol
</td><td> The protocol is not supported. For more information, see the documentation.
</td></tr>
<tr>
<td> 5000
</td><td> Resource does not exist
</td><td> The instance corresponding to the resource ID does not exist, the instance has been returned, or resource accessed belongs to other users.
</td></tr>
<tr>
<td> 5100
</td><td> Resource operation failed
</td><td> The operation on the resource failed. For detailed error information, see the `message` field. Please try again later or contact customer service for assistance.
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
</td><td> A part of the batch operation has been performed successfully. For more information, see the return value of the method.
</td></tr>
<tr>
<td> 5500
</td><td> User qualification review failed
</td><td> Failed to purchase the resource due to user qualification review failure.
</td></tr>
<tr>
<td> 6000
</td><td> Internal server error
</td><td> An error occurred inside the server. Please try again later or contact customer service for assistance.
</td></tr>
<tr>
<td> 6100
</td><td> Unsupported by current version
</td><td> The API is not supported by the current version or is under maintenance. Note: When this error occurs, first check whether the domain name of the API is correct, as the domain name may vary by module.
</td></tr>
<tr>
<td> 6200
</td><td> API temporarily inaccessible
</td><td> The current API is under maintenance and not in service. Please try again later.
</td></tr></tbody></table>