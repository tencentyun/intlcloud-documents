## Overview

If an XML Python SDK operation is successful, the system will return `dict` or `None`. If an SDK API call to request the COS service fails, the system will throw `CosClientError` (client exception) or `CosServiceError` (server exception).
- The client exception, `CosClientError`, results from unexpected interaction issues between the client and the COS server, such as a failure to connect to the server, a failure to parse the data returned by the server, or the occurrence of an IO exception when reading a local file. 
- The server exception, `CosServiceError`, occurs when the client interacts with the COS server normally, but the operation fails. For example, the client accesses a bucket that does not exist, deletes an object that does not exist, or does not have the permission to perform an operation.


## Client Exceptions
A `CosClientError` generally refers to a client error caused by issues such as timeout. When capturing such an error, you can choose to retry or perform other operations.

## Server Exceptions
A `CosServiceError` contains the detailed information returned by the server, including the status code, request ID, and error details. After such an exception is captured, it is recommended that you print out the entire exception as it contains necessary factors for troubleshooting. The following describes the member variables of the exception and provides an example of exception capturing.

| Member       | Description            | Type  |
| ----------- | ---------------- | ------ |
| request_id | Request ID, used to identify a request. It is very important for troubleshooting. | string |
| status_code | Status code in the response. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| error_code | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |
| error_msg | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | string |

#### Example of Exception Capturing

```python
from qcloud_cos import CosServiceError

except CosServiceError as e:
    e.get_origin_msg()  # Get the original error message in XML format
    e.get_digest_msg() # Get the processed error message in dict format
    e.get_status_code() # Get the HTTP error code (e.g. 4xx, 5xx)
    e.get_error_code() # Get the COS-defined error code
    e.get_error_msg() # Get a detailed description of the COS error code
    e.get_trace_id() # Get the trace_id of the request
    e.get_request_id() # Get the request_id of the request
    e.get_resource_location() # Get the URL
```

## Using the Diagnosis Tool

COS provides a self-help [diagnosis tool](https://console.cloud.tencent.com/cos5/diagnose) to help you quickly locate request problems and debug code.

#### Directions
1. Copy the request ID (`RequestId`) returned when the request error occurs.
2. Click [Diagnosis Tool](https://console.cloud.tencent.com/cos5/diagnose).
<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                Diagnosis Tool
            </div>
            <a href="https://console.cloud.tencent.com/cos5/diagnose" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to start diagnosis</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Enter `RequestId` for intelligent diagnosis and obtain basic request information, directions, and diagnosis information to quickly locate request errors.
            </div>
        </div>
    </div>
</div>
3. Enter `RequestId` and click **Diagnose**.
4. Wait and view the diagnostic result.


