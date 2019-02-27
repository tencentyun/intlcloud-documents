[//]: # (chinagitpath:XXXXX)

## Feature Description

The error code returned indicates the result of the call to a cloud API. The code of 0 indicates a successful call. Other values indicate a failure. When the call fails, you can identify the cause of error and take appropriate actions based on the list of common error codes.
Example:

```
{
    "code": 5100
}
```

## Error Codes

<table>
   <tr>
      <td>Error Code</td>
      <td>Description</td>
      <td>Reason</td>
   </tr>
   <tr>
      <td>4000</td>
      <td>Invalid request parameter.</td>
      <td>Required parameter is missing, or parameter value is in an incorrect format. For error message, see the "message" field in error description.</td>
   </tr>
   <tr>
      <td>4100</td>
      <td>Authentication failed</td>
       <td>The failure of authentication is usually caused by signature computing error. See <a href="https://cloud.tencent.com/document/api/213/6984">Signature Method</a> section in the document.</td>
   </tr>
   <tr>
      <td>4101</td>
      <td>Unauthorized access to the API.</td>
      <td>The sub-account is not authorized by the main account to access the API. Contact the main account administrator to grant the permission for the API.</td>
   </tr>
   <tr>
      <td>4102</td>
      <td>Unauthorized access to the resource.</td>
      <td>The sub-account is not authorized by the main account to access the resource. Contact the main account administrator to grant the permission for the resource.</td>
   </tr>
   <tr>
      <td>4103</td>
      <td>Unauthorized access to the resource the current API is working with.</td>
      <td>The sub-account is not authorized by the main account to access the resource the current API is working with. Contact the main account administrator to grant the permission for the resource.</td>
   </tr>
   <tr>
      <td>4104</td>
      <td>Key does not exist.</td>
      <td>The key used for the request does not exist. Verify it and try again.</td>
   </tr>
   <tr>
      <td>4105</td>
      <td>Token error.</td>
      <td>Token error.</td>
   </tr>
   <tr>
      <td>4106</td>
      <td> MFA verification failed.</td>
      <td> MFA verification failed.</td>
   </tr>
   <tr>
      <td>4110</td>
      <td>Other CAM authentication failed.</td>
      <td>Other CAM authentication failed.</td>
   </tr>
   <tr>
      <td>4300</td>
      <td>Access denied.</td>
      <td>Account is blocked or is not within the user range for the API.</td>
   </tr>
   <tr>
      <td>4400</td>
      <td>Quota exceeded.</td>
      <td>The number of requests exceeded the quota limit. For more information, see the "Request Quota" section in the document.</td>
   </tr>
   <tr>
      <td>4500</td>
      <td>Replay attack</td>
      <td>The Nonce and Timestamp parameters can ensure that each request is executed only once on the server. Therefore, the Nonce value cannot be the same as last one, and the difference between Timestamp and Tencent server time cannot be greater than 5 minutes.</td>
   </tr>
   <tr>
      <td>4600</td>
      <td>Unsupported protocol.</td>
      <td>The protocol is not supported. The current API only supports HTTPS protocol and does not support HTTP protocol.</td>
   </tr>
   <tr>
      <td>5000</td>
      <td>Resource does not exist.</td>
      <td>The instance corresponding to resource ID does not exist, or the instance has been returned, or another user's resource is accessed.</td>
   </tr>
   <tr>
      <td>5100</td>
      <td>Resource operation failed.</td>
      <td>The operation performed on the resource failed. For error message, see the "message" field in error description. Try again later or contact customer service.</td>
   </tr>
   <tr>
      <td>5200</td>
      <td>Failed to purchase the resource.</td>
      <td>The resource purchase failed. This is may be caused by unsupported instance configuration or insufficient resource.</td>
   </tr>
   <tr>
      <td>5300</td>
      <td>Insufficient balance.</td>
      <td>User account has insufficient balance. Unable to purchase or upgrade the resource.</td>
   </tr>
   <tr>
      <td>5400</td>
      <td>The operation was successful on some resources.</td>
      <td>The batch operation was successful on some resources. For more information, see the returned value of the method.</td>
   </tr>
   <tr>
      <td>5500</td>
      <td>User failed to pass identity verification.</td>
      <td>Resource purchase failed because the user failed to pass identity verification.</td>
   </tr>
   <tr>
      <td>6000</td>
      <td>Internal error with the server.</td>
      <td>An internal error occurred with the server. Try again later or contact customer service.</td>
   </tr>
   <tr>
      <td>6100</td>
      <td>Not supported in the version.</td>
      <td>The API is not supported by this version or is under maintenance. Note: When this error occurs, first check whether the domain name of the API is correct. Domain name may vary between different modules.</td>
   </tr>
   <tr>
      <td>6200</td>
      <td>API is unavailable.</td>
      <td>The API is under maintenance and is unavailable. Please try again later.</td>
   </tr>
</table>

