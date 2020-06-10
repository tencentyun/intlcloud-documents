## Overview

If a request to COS fails by calling this SDK, it will throw CosClientException (client exception) or CosServerException (server exception).
- The CosClientException results from unexpected interaction issues between the client and COS server, such as failure to connect to the server, failure to parse the data returned by the server, and the occurrence of IO exception when reading a local file.
- The CosServerException occurs when the client interacts with the COS server normally, but fails to work with COS resources. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc.


## Client Exception

Inherited from System.ApplicationException, CosClientException is used in the same way as System.ApplicationException. An additional member errorCode is also added, as shown below:

| Member | Description | Type |
| ---- | ---- | ---- |
|errorCode| Client error code, such as 10000, which indicates a parameter verification failure. For more information, see [SDK Error Codes](https://intl.cloud.tencent.com/document/product/436/30610).|int|



## Server Exception

CosServiceException contains the status code returned by the server, requestid, and error details. After an exception is captured, it is recommended to print the entire exception which provides the necessary factors for troubleshooting. Member variables of the exception are described as follows:

| Member | Description | Type |
| ------------ | ---------------------------------------- | --------- |
| requestId | Request ID to identify a request. It is very important for troubleshooting. | string |
| statusCode | Status code in the response. 4xx represents the request failure caused by the client, and 5xx represents the failure caused by the server exception. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorCode | Error code returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| errorMessage | Error message returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |

