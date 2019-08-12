## Overview

If an SDK API call to request the COS service fails (with a return code 4xx or 5xx, for example), the system will throw a Qcloud\Cos\Exception\ServiceResponseException exception.

## Server Exceptions

CosServerException contains the status code, requestid, and error details returned by the server. After an exception is captured, you are recommended to print the entire exception to get the information required for troubleshooting. Below are descriptions of exception member variables and an example of exception capture:

| Member | Description | Type |
| ----------- | ---------------- | ------ |
| requestId | Request ID, which is used to represent a request and is very important for troubleshooting | string |
| statusCode | Status code in the response. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |


### Exception Capture Example

```php
try {
   $cosClient->listBuckets() 
} catch (\Exception $e) {
    $statusCode = $e->getStatusCode(); // Get the status code
    $errorMessage = $e->getMessage(); // Get the error message
    $requestId = $e->getRequestId(); // Get the error requestId
    $errorCode = $e->getCosErrorCode(); // Get the error code
    $request = $e->getRequest(); // Get the full request
    $response = $e->getResponse(); // Get the full response
｝
```
