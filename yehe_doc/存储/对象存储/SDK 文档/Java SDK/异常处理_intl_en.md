## Overview

Whenever a COS request fails when calling this SDK, it throws a `RuntimeExcpetion`. The common SDK exceptions are `CosClientException`, `CosServiceException`, and `IllegalArgumentException`.


## Client Exception

The client exception, `CosClientException`, results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO exception when reading a local file. Inherited from `RuntimeException`, `CosClientException` has no custom member variables, and is used in the same way as `RuntimeException`.

## Server Exception

The server exception, `CosServerException`, occurs when the client interacts with the COS server normally, but the operation fails. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc. `CosServiceException` contains the status code returned by the server, the `requestid`, the error details, and so on. After an exception is captured, we recommended that you print out the entire exception as it contains necessary factors for troubleshooting. The member variables of exception are described as follows:


| Request Element | Description | Type |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId | Request ID, used to identify a request. It is very important for troubleshooting. | String |
| traceId | ID for troubleshooting | String |
| statusCode | Status code in the response. A `4XX` status code represents a request failure caused by the client, and a `5XX` status code represents a failure caused by a server exception. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorType | Enumeration type, indicating the type of exception, e.g., `Client`, `Service`, `Unknown` | ErrorType |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |

## FAQs

If you have any questions about the Java SDK, see the Java SDK section in [API and SDK FAQs](https://intl.cloud.tencent.com/document/product/436/10687).
