## Overview

If a COS request fails when calling this SDK, it will throw a `CosXmlClientError` (client error) or `CosXmlServiceError` (server error).
- The client error, `CosXmlClientError`, results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO error when reading a local file.
- The server error, `CosXmlServiceError`, occurs when the client interacts with the COS server normally, but the operation fails. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation.


## Client Errors

`CosXmlClientError` contains the defined client error code and specific error message, such as local file IO error. After such an error is captured, we recommend that you print out the entire error as it contains necessary factors for troubleshooting. The following describes the member variables of the error:

| Member | Description | Type |
| ---- | ---- | ---- |
| errorCode | Client error code, such as 10000, which indicates a parameter verification failure. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/436/30610) | int |
|message| Client error message |string|

## Server Errors

The server error, `CosXmlServiceError`, occurs when, for example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc. `CosXmlServiceError` contains the status code returned by the server, the `requestid`, the error details, and so on. After an error is captured, we recommend that you print out the entire error as it contains necessary factors for troubleshooting. The member variables of error are described as follows:

| Member | Description | Type |
| ------------ | ---------------------------------------- | --------- |
| requestId | Request ID, used to identify a request. It is very important for troubleshooting. | string |
| statusCode | Status code in the response. A `4XX` status code represents a request failure caused by the client, and a `5XX` status code represents a failure caused by a server exception. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/436/7730). | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/436/7730). | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/436/7730). | string |


## Using the Diagnosis Tool

COS provides a self-help [diagnosis tool](https://console.cloud.tencent.com/cos5/diagnose) to help you quickly locate request errors and debug the code.

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
