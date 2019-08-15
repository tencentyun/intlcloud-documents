## Overview

When an SDK call fails to request the COS service, all exceptions thrown are of RuntimeExcpetion type. Currently, common exceptions of the SDK include CosClientException, CosServiceException, and IllegalArgumentException.


## Client Exceptions

A client exception (CosClientError) is caused by the client's inability to interact with the server properly, for example, the client cannot connect to the server or parse the data returned by the server, or an IO exception occurs during reading the local file. CosClientException is inherited from RuntimeException, has no custom member variables, and can be used in the same way as RuntimeException.

## Server Exceptions

A server exception (CosServiceException) occurs when the interaction is properly completed but the operation fails, for example, the client accesses a bucket that does not exist, deletes a file that does not exist, does not have permission to perform an operation, or fails. CosServiceException contains the status code, requestid, and error details returned by the server. After an exception is captured, you are recommended to print the entire exception to get the information required for troubleshooting. Below are descriptions of exception member variables:


| Request Member | Description | Type |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId | Request ID, which is used to represent a request and is very important for troubleshooting | String |
| traceId | Trace ID for troubleshooting | String |
| statusCode | Status code in the response. 4xx indicates that the request failed due to a client exception; while 5xx indicates that the request failed due to a server exception. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| errorType | Enumeration class, indicating the type of exception. Value range: Client, Service, Unknown | ErrorType |
| errorCode | Error code returned by the body when the request fails. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| errorMessage | Error message returned by the body when the request fails. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | String    |

## FAQs

If you have any questions when using the SDK for Java, see the SDK for Java section in [FAQs](https://intl.cloud.tencent.com/document/product/436/31537).
