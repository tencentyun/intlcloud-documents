## Overview

When calling the SDK to request the COS or CI service fails, all exceptions reported are `RuntimeExcpetion`.
Common exceptions in the SDK currently include `CosClientException`, `CosServiceException`, `CIServiceException`, and `IllegalArgumentException`.

## Client Exceptions

`CosClientException` results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO exception when reading a local file. Inherited from `RuntimeException`, `CosClientException` has no custom member variables, and is used in the same way as `RuntimeException`.

## Server Exceptions

`CosServiceException` and `CIServiceException` refer to scenarios where the interaction is completed normally but the operation fails; for example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform the operation, or the server fails.
`CosServiceException` contains the status code, request ID, and error details. After such an exception is captured, we recommend you print out the entire exception as it contains necessary factors for troubleshooting. The following describes the member variables of the exception:

| Request Element | Description | Type |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId | Request ID, which is used to identify a request and is very important for troubleshooting. | String |
| traceId | ID for troubleshooting | String |
| statusCode | Status code in the response. 4xx indicates that the request failed due to a client exception. 5xx indicates that the request failed due to a server exception. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorType | Enumeration type, indicating the type of exception, such as `Client`, `Service`, and `Unknown`. | ErrorType |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |


## Using the Diagnosis Tool

CI provides a self-help [diagnosis tool](https://console.cloud.tencent.com/cos5/diagnose) to help you quickly locate request errors and debug the code.

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

If you have any questions about the Java SDK, see [FAQs](https://www.tencentcloud.com/document/product/1045/53335).

