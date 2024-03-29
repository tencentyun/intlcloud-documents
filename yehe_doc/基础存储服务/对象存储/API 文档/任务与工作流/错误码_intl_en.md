## Overview

This document describes the error codes and the error messages returned when requests fail.

## Error Response

Content-Type: application/xml

HTTP status code: 3XX, 4XX, or 5XX

#### Response body

```xml
<?xml version='1.0' encoding='utf-8' ?>
<Error>
	<Code>string</Code>
	<Message>string</Message>
	<RequestId>string</RequestId>
	<TraceId>string</TraceId>
</Error>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ------------------ | --------- |
| Error | None | All error messages | Container |

**`Error` has the following sub-nodes:**

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------ | ------------------------------------------------------------ | ------ |
| Code    | Error  | Error code, which uniquely identifies an error condition and determines the error scenario. Error codes are described in detail below. | string |
| Message | Error  | Specific error message  | string |
| RequestId | Error  | ID automatically generated by the server for a request when the request is sent, which can be used to facilitate fault locating | string |
| TraceId | Error  | ID automatically generated by the server for a request when a request error occurs, which can be used to facilitate fault locating  | string |

## Error Codes

**3XX errors**

| Error Code | Description | HTTP Status Code |
| ----------------- | ------------------------------------------------------------ | ---------------------- |
| PermanentRedirect | The resource has been permanently relocated. Please use the `HTTP Location` response header to get redirected to the correct location | 301 Moved Permanently |
| TemporaryRedirect | The resource has been temporarily relocated. Please use the `HTTP Location` response header to get redirected to the correct location | 307 Temporary Redirect |

**4xx errors**

| Error Code | Description | HTTP Status Code |
| -------------------------- | ------------------------------------------------------------ | --------------------------------- |
| InvalidArgument            | Some parameters of the request do not meet requirements.                                     | 400 Bad Request                   |
| MissingContent             | Packet missing.                                                     | 400 Bad Request                   |
| InvalidContent             | The packet sent is in incorrect format or is inconsistent with the value of [Content-MD5](https://intl.cloud.tencent.com/document/product/1045/43609). | 400 Bad Request                   |
| InvalidHost                | [Host](https://intl.cloud.tencent.com/document/product/1045/43609) authentication failed. | 400 Bad Request                   |
| ResourceNotFound           | The specified input resource does not exist.                                         | 400 Bad Request                   |
| ResourceAccessDenied       | You have no permission to operate the specified resource. Check whether the permission is granted.                       | 400 Bad Request                   |
| ResourceDownloadFailed     | Downloading the specified input resource failed.                                        | 400 Bad Request                   |
| CIRoleNotExist             | The CI role `CI_QCSRole` does not exist.                                     | 400 Bad Request                   |
| ResourceNotSupported       | The file is faulty or unsupported.                                           | 400 Bad Request                   |
| MissingAuthorization       | [Authorization](https://intl.cloud.tencent.com/document/product/1045/43609) missing. | 401 Unauthorized                  |
| InvalidAuthorization       | Incorrect format of [Authorization](https://intl.cloud.tencent.com/document/product/1045/43609). | 401 Unauthorized                  |
| AccessDenied               | No permission.                                                     | 401 Unauthorized                  |
| SecretidNotExist           | The key does not exist.                                                 | 401 Unauthorized                  |
| SignatureExpired           | The signature has expired.                                                   | 401 Unauthorized                  |
| AccessDenied               | The operation is prohibited.                                                   | 403 Forbidden                     |
| MediaBucketAlreadyBinded   | The bucket is already bound.                                           | 403 Forbidden                     |
| QueueSaturated             | The queue is full.                                                   | 403 Forbidden                     |
| QueuePaused                | The queue is suspended.                                                 | 403 Forbidden                     |
| InvalidUrl                 | The request URL format is incorrect.                                        | 404 Not Found                     |
| AuditingJobNotFound        | The audit job does not exist.                                                | 404 Not Found                     |
| MissingContentLength       | The [Content-Length](https://intl.cloud.tencent.com/document/product/1045/43609) request header is missing. | 411 Length Required               |
| InvalidContent             | The sent packet is too large.                                               | 413 Payload Too Large             |
| SlowDown                   | Please decrease the access frequency.                                               | 429 Too Many Requests             |
| UnavailableForLegalReasons | Unavailable due to legal reasons. Please [submit a ticket](https://console.intl.cloud.tencent.com/workorder). | 451 Unavailable For Legal Reasons |

**5xx errors**

| Error Code | Description | HTTP Status Code |
| ------------------ | -------------------- | ----------------------- |
| InternalError | Internal server error. | 500 Internal Server |
| NotImplemented | The request has not been implemented. | 501 Not Implemented |
| ServiceUnavailable | The service is temporarily unavailable. Please try again. | 503 Service Unavailable |
