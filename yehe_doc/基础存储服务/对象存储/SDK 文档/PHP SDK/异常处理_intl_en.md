## Overview

When you fail to request COS service via the SDK, such as getting 4xx or 5xx return code, the system will throw an exception (Qcloud\Cos\Exception\ServiceResponseException).


## Server Exceptions

CosServiceException contains the status code returned by the server, requestId, error details, etc. After an exception is caught, it is recommended to print the entire exception to get the necessary information for troubleshooting. The following describes member variables of an exception and an example of catching an exception:

| Member       | Description            | Type  |
| ----------- | ---------------- | ------ |
| requestId | Request ID which identifies a request. It is very important for troubleshooting. | string |
| statusCode | Status code in the response. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |


#### Example of Exception Capturing

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
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


## Using the Diagnosis Tool

COS provides a self-help [diagnosis tool](https://console.cloud.tencent.com/cos5/diagnose) to help you quickly locate request problems and debug code.

#### Directions
1. Copy the request ID (`RequestId`) returned when the request error occurs.
2. Click [Diagnosis Tool](https://console.cloud.tencent.com/cos5/diagnose).
<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                Diagnosis Tool
            </div>
            <a href="https://console.cloud.tencent.com/cos5/diagnose" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to start diagnosis</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Enter `RequestId` for intelligent diagnosis and obtain basic request information, directions, and diagnosis information to quickly locate request errors.
            </div>
        </div>
    </div>
</div>
3. Enter `RequestId` and click **Diagnose**.
4. Wait and view the diagnostic result.


