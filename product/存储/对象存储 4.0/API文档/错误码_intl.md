## Overview

This document describes the error codes and the error messages returned when requests fail.

## Format of Returned Error Message

### Response headers

Content-Type：application/xml

HTTP status codes: 3xx, 4xx, or 5xx

### Response content

**Syntax format**

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Error>
  <Code>[Error code]</Code>
  <Message>[Error message]</Message>
  <Resource>[Resource address]</Resource>
  <RequestId>[Request ID]</RequestId>
  <TraceId>[Error ID]</TraceId>
</Error>
```
<style  rel="stylesheet"> table th:nth-of-type(1) { width: 200px; }</style>

**Element description**

| Element Name | Description | Type |
| --------- | ---------------------------------------- | --------- |
| Error | Contains all error information | Container |
| Code | Error code, which uniquely identifies an error condition and determines the error scenario. Error codes are described in detail below. | String |
| Message | Contains detailed error message | String |
| Resource | Resource address: Bucket address or Object address | String |
| RequestId | The unique ID generated automatically by the server when a request is sent. It can be used to quickly locate any problem occurred. | String |
| TraceId | The unique ID generated automatically by the server when an error occurs with the request. It can be used to quickly locate any problem occurred. One trace-id corresponds to one request-id. | String |

## Error Codes

**3XX errors**

| Error Code | Description | HTTP Status Code |
| ----------------- | ---------------------------------------- | --------------------- |
| PermanentRedirect | This resource has been moved to another location permanently. Redirect to a new location by using HTTP Location. | 301 Moved Permanently |
| TemporaryRedirect | This resource has been moved to another location temporarily. Redirect to a new location by using HTTP Location. | 302 Moved Temporarily |
| Redirect | Temporary redirection | 307 Moved Temporarily |
| TemporaryRedirect | You are redirected temporarily during DNS update | 307 Moved Temporarily |

**4XX Errors**

| Error Code | Description | HTTP Status Code |
| ----------------------------------- | --------------------------------- | ----------------------------------- |
| InvalidSHA1Digest | sha1 of the request content is invalid | 400 Bad Request |
| NoSuchUpload |	The uploadid specified for the multipart upload does not exist | 400 Bad Request |
| InvalidPart | One or more parts cannot be found | 400 Bad Request |
| InvalidPartOrder | The list of parts was not in ascending order | 400 Bad Request |
| ObjectNotAppendable | Specified file is not appendable | 400 Bad Request |
| AppendPositionErr | The length of the file is inconsistent with the append position | 400 Bad Request |
| NoSuchVersion | Specified version does not exist | 400 Bad Request |
| NoLifecycle | Lifecycle does not exist | 400 Bad Request |
| PreconditionFailed | At least one of the preconditions you specified did not hold | 400 Bad Request |
| UnexpectedContent | The content is not supported for the request | 400 Bad Request |
| MultiBucketNotSupport | Only one destination Bucket can be configured in cross-origin replication | 400 Bad Request |
| NotSupportedStorageClass | The specified storage type is invalid | 400 Bad Request |
| BadDigest | The x-cos-SHA-1 value you provided does not match that received by the server | 400 Bad Request |
| EntityTooSmall | Your proposed upload is smaller than the minimum allowed object size, which usually happens in multipart uploads. | 400 Bad Request |
| EntityTooLarge | Your proposed upload exceeds the maximum allowed object size | 400 Bad Request |
| ImcompleteBody | The actual content length of the request is inconsistent with the specified Content-Lengt. | 400 Bad Request |
| IncorrectNumberOfFilesInPostRequest | Only one file is allowed to be uploaded at a time for a Post request | 400 Bad Request |
| InlineDataTooLarge | Inline data exceeds the maximum allowed size | 400 Bad Request |
| InvalidArgument | The request parameter is invalid | 400 Bad Request |
| InvalidBucketName | The Bucket name is invalid | 400 Bad Request |
| InvalidDigest | The x-cos-SHA-1 value is invalid | 400 Bad Request |
| InvalidPart | One or more parts cannot be found or SectionID is invalid | 400 Bad Request |
| InvalidPolicyDocunment | Policy configuration file is invalid | 400 Bad Request |
| InvalidURI | The URI is invalid | 400 Bad Request |
| KeyTooLong | Custom header is too long | 400 Bad Request |
| MalformedACLError | The specified ACL policy does not comply with XML syntax | 400 Bad Request |
| MalformedPOSTRequest | The body content of the POST request is invalid | 400 Bad Request |
| MalformedXML | The body in XML format does not comply with XML syntax | 400 Bad Request |
| MaxMessageLengthExceeded | Request is too long | 400 Bad Request |
| MaxPostPreDataLengthExceededError | The POST request fields preceding the upload file were too large, which usually happens in multipart upload operations. | 400 Bad Request |
| MatadataTooLarge | The size of metadata exceeds the maximum allowed size | 400 Bad Request |
| MissingRequestBodyError | Request body is missing | 400 Bad Request |
| MissingSecurityHeader | Required header is missing | 400 Bad Request |
| MissingContentMD5 | Content-MD5 is missing in request header | 400 Bad Request |
| MissingAppid | Appid is missing in request header | 400 Bad Request |
| MissingHost | Host is missing in request header | 400 Bad Request |
| RequestIsNotMultiPartContent | The Content-Type of the POST request is invalid | 400 Bad Request |
| RequestTimeOut | Read timed out. Check your network speed or reduce the number of concurrent uploads. | 400 Bad Request |
| TooManyBucket | The number of Buckets exceeds the limit of 200 | 400 Bad Request |
| UnexpectedContent | The content is not supported for the request | 400 Bad Request |
| UnresolvableGrantByUID | The provided UID does not exist | 400 Bad Request |
| UserKeyMustBeSpecified | The path must be specified for the POST operation performed against a Bucket | 400 Bad Request |
| ExpiredToken | Signature string expired | 403 Forbidden |
| AccessDenied | Access denied due to invalid signature or permission | 403 Forbidden |
| AccountProblem | This operation has been denied by your account | 403 Forbidden |
| InvaildAccessKeyId | AccessKey does not exist | 403 Forbidden |
| InvalidObjectState | Request content conflicts with the attribute of the Object | 403 Forbidden |
| InvalidSecurity | Signature string is invalid | 403 Forbidden |
| RequestTimeTooSkewed | The difference between the request time and the server's time is too large | 403 Forbidden |
| SignatureDoesNotMatch | Incorrect signature | 403 Forbidden |
| NoSuchBucket | The specified Bucket does not exist | 404 Not Found |
| NoSuchUpload | The specified multipart upload does not exist | 404 Not Found |
| NoSuchBucket | The specified Bucket policy does not exist | 404 Not Found |
| MethodNotAllowed | The HTTP method is not supported for this resource | 405 Method Not Allowed |
| BucketAlreadyExists | BucketName specified by CreateBucket is already in use. Select another BucketName. | 409 Conflict |
| BucketNotEmpty | Delete files and unfinished multipart upload tasks before performing DeleteBucket operation | 409 Conflict |
| InvalidBucketState | Bucket status conflicts with operation request. For example, multi-version management conflicts with cross-origin replication. | 409 Conflict |
| OperationAborted | The operation is not supported for the specified resource, or the resource being downloaded is incomplete or damaged during transfer. | 409 Conflict |
| MissingContentLength | The header "Content-Length" is missing | 411 Length Required |
| PreconditionFailed | Precondition matching failed | 412 Precondition |
| InvalidRange | Requested file range is invalid | 416 Requested Range Not Satisfiable |



**5XX Errors**

| Error Code | Description | HTTP Status Code |
| ------------------ | ---------------- | ----------------------- |
| InternalError | Internal error occurred with the server | 500 Internal Server |
| NotImplemented | A method in the Header cannot be implemented | 501 Not Implemented |
| ServiceUnavailable | Internal error occurred with the server. Try again. | 503 Service Unavailable |
| SlowDown | Reduce your request rate | 503 Slow Down |

**Other Errors**

| Error Code | Description | HTTP Status Code |
| ----------------------- | ---------- | ------- |
| InvaildAddressingHeader | Anonymous access is required | N/A |


