## Introduction

If the call to an SDK API for requesting the COS service fails, CosClientException (client exception) or CosServerException (server exception) occurs.
- CosClientException is caused by the client's inability to interact with the COS server normally, such as failure to connect to the server, failure to parse the data returned by the server, and the occurrence of I/O exception when reading a local file.
- CosServerException means that the client interacts with the COS server normally, but fails to work with COS resources. For example, the client accesses a bucket that does not exist, deletes a file that does not exist, or does not have the permission to perform an operation, etc.


## Client Exception

Inherited from System.ApplicationException, CosClientException is used in the same way as System.ApplicationException. An additional member errorCode is also added, as shown below:

| Member | Description | Type |
| ---- | ---- | ---- |
| errorCode | Client error code. For example, 10000 indicates that the parameter verification failed. | int |



## Server Exception

CosServiceException contains the status code returned by the server, requestid, error details, and so on. After an exception is captured, it is recommended to print the entire exception. The exception contains the necessary troubleshooting factors. Member variables of exception are described as follows:

| Member | Description | Type |
| ------------ | ---------------------------------------- | --------- |
| requestId | Request ID to specify a request. It is very important for troubleshooting. | string |
| statusCode | Status code of the response. 4xx represents the request failure caused by the client, and 5xx represents the failure caused by the server exception. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730). | string |
| errorCode | Error code returned by body when request fails. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730). | string |
| errorMessage | Error message returned by body when request fails. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730). | string |


