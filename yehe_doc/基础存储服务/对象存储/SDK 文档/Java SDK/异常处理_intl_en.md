## Overview

Whenever a COS request fails when calling this SDK, the system throws a `RuntimeExcpetion`. Common SDK exceptions are `CosClientException`, `CosServiceException`, and `IllegalArgumentException`.


## Client Exceptions

The client exception, `CosClientException`, results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO exception when reading a local file. Inherited from `RuntimeException`, `CosClientException` has no custom member variables, and is used in the same way as `RuntimeException`.

## Server Exceptions

The server exception, `CosServerException`, occurs when the client interacts with the COS server normally, but the operation fails. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc. `CosServiceException` contains the status code returned by the server, the `requestid`, the error details, and so on. After an exception is captured, we recommended that you print out the entire exception as it contains necessary factors for troubleshooting. The member variables of exception are described as follows:


| Request Element | Description | Type |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId | Request ID, used to identify a request. It is very important for troubleshooting. | String |
| traceId | ID for troubleshooting | String |
| statusCode | Status code in the response. 4xx indicates that the request failed due to a client exception. 5xx indicates that the request failed due to a server exception. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorType | Enumeration type, indicating the type of exception, e.g., `Client`, `Service`, `Unknown` | ErrorType |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |


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


## FAQs

If you have any questions about Java SDK, see the Java SDK section in [FAQs](https://intl.cloud.tencent.com/document/product/436/38956).

