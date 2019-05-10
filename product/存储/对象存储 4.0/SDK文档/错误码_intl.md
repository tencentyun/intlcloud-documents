## Overview

The errors occurring during the use of the COS API service provided by SDK can be divided into client errors and errors returned by the server.

- Errors returned by the server refer to the errors returned when the server processes some client requests that do not meet the requirements. For example, access to a file that does not exist, or no access to a file. For more information on the error codes returned by the server, see [API Error Codes](https://cloud.tencent.com/document/product/436/7730).
- Client errors refer to network exception, IO exception during file read/write, parameter verification failure, etc.

This document describes the error codes defined by the client.

## Error Codes
The supported SDKs are Android and iOS SDKs.

| Error Code | Error Message | Error Description |
| ------ |--------- | ---- |
| 10000 | InvalidArgument | Parameter verification failed. For example, the required parameter is empty. |
| 10001 | InvalidCredentials | Key information verification failed. For example, the key is empty. |
| 10002 | BadRequest | Incorrect SDK configuration. For example, APPID or region is not correct. |
| 10003 | SinkSourceNotFound | Incorrect input source or output source. For example, the uploaded file does not exist. |
| 10004 | UnsupportOperation | Unsupported operation |
| 20000 | InternalError | Internal error, such as parsing the data in xml format failed. |
| 20001 | ServerError | Service error, such as data in non-xml format is returned. |
| 20002 | IOError | IO exception during stream read/write, such as IO exception during file read/write. |
| 20003 | NetworkError | Network exception, such as network unavailability, and DNS resolution failure. |
| 20004 | DataIntegrityError | Data integrity verification failed. |
| 30000 | UserCancelled | The user has cancelled the request. |
| 30001 | AlreadyFinished | The request has been executed. |

