## Overview

When you fail to request COS service via the SDK, such as getting 4xx or 5xx return code, the system will throw an exception (Qcloud\Cos\Exception\ServiceResponseException).

## Server exceptions

CosServiceException contains the status code returned by the server, requestId, error details, etc. After an exception is caught, it is recommended to print the entire exception to get the necessary information for troubleshooting. The following describes member variables of an exception and an example of catching an exception:

| Member       | Description            | Type  |
| ----------- | ---------------- | ------ |
| requestId | Request ID which identifies a request. It is very important for troubleshooting. | string |
| statusCode | Status code in the response. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |


#### Example of Exception Catching

```php
try {
   $cosClient->listBuckets() 
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    $statusCode = $e->getStatusCode(); // Get the error code
    $errorMessage = $e->getMessage(); // Get the error message
    $requestId = $e->getRequestId(); // Get the requestId corresponding to the error
    $errorCode = $e->getCosErrorCode(); // Get the error name
    $request = $e->getRequest(); // Get the entire request
    $response = $e->getResponse(); // Get the entire response
    echo ($e);
} catch (\Exception $e) {

}
```
>! If you install the SDK using Phar or the source code, the error messages returned will be clearer. If you install with Composer and the error messages returned do not meet your requirements, you can customize some error messages by modifying `vendor/guzzlehttp/guzzle-services/src/SchemaValidator.php`.
>
