## Overview

If an SDK API call to request the COS service fails, the system will throw CosXmlClientException (client exception) or CosXmlServiceException (server exception).
- CosXmlClientException is caused by the client's inability to interact with the COS server properly, for example, the client cannot connect to the server or parse the data returned by the server, or an IO exception occurs during reading the local file.
- CosXmlServiceException is caused by failures in COS resource operations (the client can interact with the COS server normally though), for example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have permission to perform an operation.


## Client Exceptions

CosClientException is integrated from Exception and can be used in the same way as Exception. It has an additional member "errorCode" as shown below:

| Member | Description | Type |
| ---- | ---- | ---- |
|errorCode| Client error code, such as 10000 indicating that the parameter verification failed. For more information, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610) |int|



## Server Exceptions

CosXmlServiceException is thrown when the client accesses a bucket that does not exist, deletes a file that does not exist, does not have permission to perform an operation, or fails. It contains the status code, requestid, and error details returned by the server. After an exception is captured, you are recommended to print the entire exception to get the information required for troubleshooting. Below are descriptions of exception member variables:

| Member | Description | Type |
| ------------ | ---------------------------------------- | --------- |
| requestId | Request ID, which is used to represent a request and is very important for troubleshooting | string |
| statusCode | Status code in the response. 4xx indicates that the request failed due to a client exception; while 5xx indicates that the request failed due to a server exception. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [COS Error Messages](https://intl.cloud.tencent.com/document/product/436/7730) | string |

