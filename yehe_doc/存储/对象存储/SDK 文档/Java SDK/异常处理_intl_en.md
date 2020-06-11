## Overview

Whenever a request to COS fails by calling this SDK, it throws RuntimeExcpetion. The common SDK exceptions are CosClientException, CosServiceException, and IllegalArgumentException.


## Client Exception

The client exception CosClientException results from server interaction failures caused by unexpected client issues such as failure to connect to the server, failure to parse the data returned by the server, and the occurrence of IO exception when reading a local file. Inherited from RuntimeException, CosClientException has no custom member variables, and is used in the same way as RuntimeException.

## Server Exception

The server exception CosServiceException occurs in scenarios where the interaction is completed but the operation failed. For example, the client accesses a bucket that does not exist, delete a file that does not exist, or does not have the permission to perform an operation, or the server failed. CosServiceException contains the status code returned by the server, requestid, error details, and so on. After an exception is captured, it is recommended to print the entire exception. The exception contains the necessary troubleshooting factors. Member variables of exception are described as follows:


| Request Element | Description                                                        | Type      |
| ------------ | ------------------------------------------------------------ | --------- |
| requestId | Request ID that identifies a request. It is very important for troubleshooting. | String |
| traceId | ID for troubleshooting | String |
| statusCode | Status code of the response. 4xx represents the request failure caused by the client, and 5xx represents the failure caused by the server exception. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorType | Enumeration type, indicating the type of exception (Client, Service, Unknown) | ErrorType |
| errorCode | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |
| errorMessage | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | String |

## FAQs

If you have any questions about Java SDK, see the Java SDK section in [FAQs](https://intl.cloud.tencent.com/document/product/436/10687).
