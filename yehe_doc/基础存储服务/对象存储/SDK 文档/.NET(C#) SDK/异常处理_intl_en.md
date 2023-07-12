## Overview

If a COS request fails when calling this SDK, it will throw a `CosClientException` (client exception) or `CosServerException` (server exception).
- The `CosClientException` results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO exception when reading a local file, etc.
- The `CosServerException` occurs when the client interacts with the COS server normally, but the operation fails. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc.


## Client Exceptions

Inherited from `System.ApplicationException`, `CosClientException` is used in the same way as `System.ApplicationException`. An additional member errorCode is also added, as shown below:

| Member | Description | Type |
| ---- | ---- | ---- |
| errorCode | Client error code, such as 10000, which indicates a parameter verification failure. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/30610) | int |


## Server Exceptions

A `CosServiceException` contains the status code returned by the server, the `requestid`, and the error details. After an exception is captured, we recommended that you print out the entire exception as it contains necessary factors for troubleshooting. The member variables of the exception are described as follows:

| Member | Description | Type |
| ------------ | ---------------------------------------- | --------- |
| requestId | Request ID, used to identify a request. It is very important for troubleshooting. | string |
| statusCode | Status code in the response. A `4XX` status code represents a request failure caused by the client, and a `5XX` status code represents a failure caused by a server exception. For more information, see [COS Error Codes](https://cloud.tencent.com/document/product/436/7730). | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |


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


