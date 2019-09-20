>**This is a legacy API and may be deprecated in the future. It is currently not displayed on the left sidebar. We recommend using [API Category](https://intl.cloud.tencent.com/document/api/213/15689), which is more standardized and has much lower access latency [API Category](https://intl.cloud.tencent.com/document/api/213/15689).**
>


## Feature Description

The error code in the returned result summarizes the result of the call and the execution of a TencentCloud API. `Code` is the common error code applicable to the APIs of all Tencent Cloud products. Any code other than 0 indicates that the request was not properly executed. Users can identify the cause of the error and take appropriate actions based on the following list of common error codes.
For example:

```
{
    "code": "5100"
}
```



## Common Error Codes

<table>
   <tr>
      <Td>Error Code</td>
      <td>Description</td>
      <td>Action</td>
   </tr>
   <tr>
      <td>4000</td>
      <td>Invalid request parameter</td>
      <td> A required parameter is missing or the parameter value is incorrectly formatted. For detailed error information, see the `message` field</td>
   </tr>
   <tr>
      <td>4100</td>
      <td>Authentication failed</td>
       <td>Signature authentication failure is usually caused by errors in signature calculation</td>
   </tr>
   <tr>
      <td>4101</td>
      <td>No API access authorization</td>
      <td>The sub-account is not authorized by the main account to access this API. Please contact the main account admin for permission to access this API</td>
   </tr>
   <tr>
      <td>4102</td>
      <td>No authorization to access resources</td>
      <td>The sub-account is not authorized by the main account to access the specified resource. Please contact the main account admin for permission to access the resource</td>
   </tr>
   <tr>
      <td>4103</td>
      <td>No authorization to access resources operated by the current API</td>
      <td>The sub-account is not authorized by the main account to access the specified resource operated by this API. Please contact the main account admin for permission to access the resource</td>
   </tr>
   <tr>
      <td>4104</td>
      <td>The key does not exist</td>
      <td>The key used for the request does not exist. Please confirm and try again</td>
   </tr>
   <tr>
      <td>4105</td>
      <td>Incorrect token</td>
      <td>The token is incorrect</td>
   </tr>
   <tr>
      <td>4106</td>
      <td>MFA verification failed</td>
      <td>MFA verification failed</td>
   </tr>
   <tr>
      <td>4110</td>
      <td>Other CAM authentication failures</td>
      <td>Other CAM authentication failures</td>
   </tr>
   <tr>
      <td>4300</td>
      <td>Access denied</td>
      <td>The account is blocked or not authorized to use the API</td>
   </tr>
   <tr>
      <td>4400</td>
      <td>Quota exceeded</td>
      <td>The number of requests exceeds the quota limit. Please use <a href = https://console.cloud.tencent.com/workorder/category?level1_id=141&level2_id=645&source=0&data_title=%E6%B4%BB%E5%8A%A8%E9%98%B2%E5%88%B7AA&level3_id=647&radio_title=%E5%9C%BA%E6%99%AF%E5%92%A8%E8%AF%A2&queue=3&scene_code=16593&step=2 >Submit Ticket</a> to solve the issue</td>
   </tr>
   <tr>
      <td>4500</td>
      <td>Replay attack</td>
      <td>The `Nonce` and `Timestamp` parameters ensure that each request will be executed only once on the server. The `Nonce` parameter must be unique, and the difference between `Timestamp` and the Tencent server time should not be greater than five minutes</td>
   </tr>
   <tr>
      <td>4600</td>
      <td>Unsupported protocol</td>
      <td>The protocol is not supported. The current API supports HTTPS protocol but not HTTP</td>
   </tr>
   <tr>
      <td>5000</td>
      <td>Resource does not exist</td>
      <td>The instance corresponds to the resource ID does not exist, the instance has been returned or resource accessed belongs to other users</td>
   </tr>
   <tr>
      <td>5100</td>
      <td>Resource operation failed</td>
      <td>The operation on the resource failed. For detailed error message, see the `message` field. Please try again later or contact customer service for assistance</td>
   </tr>
   <tr>
      <td>5200</td>
      <td>Resource purchase failed</td>
      <td>Failed to purchase the resource. Possible causes include unsupported instance configuration or insufficient resources</td>
   </tr>
   <tr>
      <td>5300</td>
      <td>Insufficient balance</td>
      <td>Insufficient balance in user account to complete the purchase or upgrade</td>
   </tr>
   <tr>
      <td>5400</td>
      <td>Partial execution success</td>
      <td>A part of the batch operation has been successfully executed. For more information, see the returned value of the method</td>
   </tr>
   <tr>
      <td>5500</td>
      <td>User qualification review failed</td>
      <td>Failed to purchase the resource due to user qualification review failure</td>
   </tr>
   <tr>
      <td>6000</td>
      <td>Internal server error</td>
      <td>An error occurred inside the server. Please try again later or contact customer service for assistance</td>
   </tr>
   <tr>
      <td>6100</td>
      <td>Unsupported by current version</td>
      <td>The API is not supported by the current version or is under maintenance. Note: When this error occurs, first check whether the domain name of the API is correct, as the domain name may vary by module</td>
   </tr>
   <tr>
      <td>6200</td>
      <td>API temporarily inaccessible</td>
      <td>The current API is under maintenance or not in service. Please try again later</td>
   </tr>
</table>
