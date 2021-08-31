>? **This is a legacy API and may be deprecated in the future. We recommend using <a href="https://intl.cloud.tencent.com/document/product/214/33789" target="_blank">CLB API 3.0</a>. The updated version is more standardized with significantly reduced access latency.**
>


## Features

The `code` (error code) in the response body indicates the result of the call to a TencentCloud API. It is a common error code applicable to all APIs. If `code` is 0, the call succeeded; otherwise, the call failed, and you can determine the cause of the error and take corresponding actions based on the list of common error codes.
Sample:

```
{
    "code": "5100"
}
```



## Common Error Codes

<table>
   <tr>
      <td>Error Code</td>
      <td>Description</td>
      <td>Action</td>
   </tr>
   <tr>
      <td>4000</td>
      <td>Invalid request parameter</td>
      <td> A required parameter is missing or the parameter value is incorrectly formatted. For error message, see the `message` field in error description.</td>
   </tr>
   <tr>
      <td>4100</td>
      <td>Identity verification failed</td>
       <td>Identity verification error. It’s usually caused by errors in signature calculation.</td>
   </tr>
   <tr>
      <td>4101</td>
      <td>Unauthorized API calls</td>
      <td>The sub-account is not authorized by the root account to use this API. Please contact the root account admin for the permission.</td>
   </tr>
   <tr>
      <td>4102</td>
      <td>Unauthorized access to resources</td>
      <td>The sub-account is not authorized by the root account to access the specified resource. Please contact the root account admin for the permission.</td>
   </tr>
   <tr>
      <td>4103</td>
      <td>Unauthorized access to resources under the current API</td>
      <td>The sub-account is not authorized by the root account to access the specified resource operated on by this API. Please contact the root account admin for the permission.</td>
   </tr>
   <tr>
      <td>4104</td>
      <td>The key does not exist</td>
      <td>The key used for the request does not exist. Please check and try again.</td>
   </tr>
   <tr>
      <td>4105</td>
      <td>Incorrect token</td>
      <td>The token is incorrect.</td>
   </tr>
   <tr>
      <td>4106</td>
      <td>MFA authentication failed</td>
      <td>MFA authentication failed.</td>
   </tr>
   <tr>
      <td>4110</td>
      <td>Other CAM authentication failed</td>
      <td>Other CAM authentication failed./td>
   </tr>
   <tr>
      <td>4300</td>
      <td>Access denied</td>
      <td>The account is blocked or unauthorized to use the API.</td>
   </tr>
   <tr>
      <td>4400</td>
      <td>Quota exceeded</td>
      <td>The number of requests exceeded the quota limit. Please <a href = https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=645&source=0&data_title=%E6%B4%BB%E5%8A%A8%E9%98%B2%E5%88%B7AA&level3_id=647&radio_title=%E5%9C%BA%E6%99%AF%E5%92%A8%E8%AF%A2&queue=3&scene_code=16593&step=2 >submit a ticket</a> for assistance.</td>
   </tr>
   <tr>
      <td>4500</td>
      <td>Replay attack</td>
      <td>The `Nonce` and `Timestamp` parameters ensure that each request will be executed only once on the server. The `Nonce` value must be unique, and the difference between `Timestamp` and the Tencent server time should not be greater than 5 minutes.</td>
   </tr>
   <tr>
      <td>4600</td>
      <td>Unsupported protocol</td>
      <td>The protocol is not supported. The current API only supports HTTPS protocol and does not support HTTP protocol.</td>
   </tr>
   <tr>
      <td>5000</td>
      <td>The resource does not exist</td>
      <td>The instance corresponding to the resource ID does not exist, or the instance has been returned, or resource accessed belongs to other users.</td>
   </tr>
   <tr>
      <td>5100</td>
      <td>Resource operation failed</td>
      <td>The operation performed on the resource failed. For error message, see the `message` field in error description. Try again later or contact customer service.</td>
   </tr>
   <tr>
      <td>5200</td>
      <td>Resource purchase failed</td>
      <td>Failed to purchase the resource. This may be caused by unsupported instance configuration or insufficient resources..</td>
   </tr>
   <tr>
      <td>5300</td>
      <td>Insufficient balance</td>
      <td>Failed to purchase or upgrade the resource due to insufficient balance.</td>
   </tr>
   <tr>
      <td>5400</td>
      <td>Partially executed</td>
      <td>The batch operation was successful on some resources. For more information, see the returned value of the function.</td>
   </tr>
   <tr>
      <td>5500</td>
      <td>User qualification review failed</td>
      <td>Failed to purchase the resource due to user qualification review failure.</td>
   </tr>
   <tr>
      <td>6000</td>
      <td>Internal server error</td>
      <td>An internal error occurred with the server. Try again later or contact customer service.</td>
   </tr>
   <tr>
      <td>6100</td>
      <td>Unsupported version</td>
      <td>The API version is not supported or is under maintenance. Note: when this error occurs, first check whether the domain name of the API is correct, as the domain name may vary by module.</td>
   </tr>
   <tr>
      <td>6200</td>
      <td>API temporarily inaccessible</td>
      <td>The current API is under maintenance and not in service. Please try again later.</td>
   </tr>
</table>
