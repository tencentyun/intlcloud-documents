## Overview

If an operation in the COS XML SDK for Python succeeds, a dict or None will be returned. If an SDK API call to request the COS service fails, the system will throw CosClientError (client exception) or CosServiceError (server exception).
- CosClientError is caused by the client's inability to interact with the COS server properly, for example, the client cannot connect to the server or parse the data returned by the server, or an IO exception occurs during reading the local file.
- CosServiceError is caused by failures in COS resource operations (the client can interact with the COS server normally though), for example, the client accesses a bucket that does not exist, deletes an object that does not exist, or does not have permission to perform an operation.

## Client Exceptions
CosClientError generally refers to a client error caused by, for example, a timeout. After it is captured, you can retry or do something else.

## Server Exceptions
CosServerException contains the specific information returned by the server, including the status code, requestid, and error details returned by the server. After an exception is captured, you are recommended to print the entire exception to get the information required for troubleshooting. Below are descriptions of exception member variables and an example of exception capture.

| Member | Description | Type |
| ----------- | ---------------- | ------ |
| request_id | Request ID, which is used to uniquely identify a request and is very important for troubleshooting | string |
| status_code | Status code in the response. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| error_code | Error code returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |
| error_msg | Error message returned by the body when the request fails. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | string |

### Exception Capture Example

```python
except CosServiceError as e:
    e.get_origin_msg()  # Get the original error message in XML format
    e.get_digest_msg()  # Get the processed error message in dict format
    e.get_status_code() # Get the HTTP error code (e.g., 4XX and 5XX)
    e.get_error_code()  # Get the error code defined by COS
    e.get_error_msg()   # Get the error message of the COS error code
    e.get_trace_id()    # Get the trace_id of the request
    e.get_request_id()  # Get the request_id of the request
    e.get_resource_location() # Get the URL address
```
