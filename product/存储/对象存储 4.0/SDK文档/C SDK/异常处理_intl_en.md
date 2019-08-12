## Overview

When an SDK call fails, the result information is included in the cos_status_t structure returned by the API.

The correct way to use each API in the SDK is as follows. For the sake of brevity, the document includes only samples of API usage but not specific exception troubleshooting.

```cpp
cos_status_t *s = NULL;
s = cos_put_object_from_file(options, &bucket, &object, &file, &headers, &resp_headers);
if (!s && !cos_status_is_ok(s)) {
		// Output logs of exceptions and process as needed
		cos_warn_log("failed to put object from file", buf);
		if (s->error_code) cos_warn_log("status->error_code: %s", s->error_code);
		if (s->error_msg) cos_warn_log("status->error_msg: %s", s->error_msg);
		if (s->req_id) cos_warn_log("status->req_id: %s", s->req_id);
}
```

## Client Exceptions

When the code member value in the cos_status_t structure is below 0, an SDK client error has occurred. For the error codes and messages, see the definition of cos_error_code_e.

```cpp
typedef enum {
		COSE_OK = 0,
		COSE_OUT_MEMORY = -1000,
		COSE_OVER_MEMORY = -999,
		COSE_FAILED_CONNECT = -998,
		COSE_ABORT_CALLBACK = -997,
		COSE_INTERNAL_ERROR = -996,
		COSE_REQUEST_TIMEOUT = -995,
		COSE_INVALID_ARGUMENT = -994,
		COSE_INVALID_OPERATION = -993,
		COSE_CONNECTION_FAILED = -992,
		COSE_FAILED_INITIALIZE = -991,
		COSE_NAME_LOOKUP_ERROR = -990,
		COSE_FAILED_VERIFICATION = -989,
		COSE_WRITE_BODY_ERROR = -988,
		COSE_READ_BODY_ERROR = -987,
		COSE_SERVICE_ERROR = -986,
		COSE_OPEN_FILE_ERROR = -985,
		COSE_FILE_SEEK_ERROR = -984,
		COSE_FILE_INFO_ERROR = -983,
		COSE_FILE_READ_ERROR = -982,
		COSE_FILE_WRITE_ERROR = -981,
		COSE_XML_PARSE_ERROR = -980,
		COSE_UTF8_ENCODE_ERROR = -979,
		COSE_CRC_INCONSISTENT_ERROR = -978,
		COSE_FILE_FLUSH_ERROR = -977,
		COSE_FILE_TRUNC_ERROR = -976,
		COSE_UNKNOWN_ERROR = -100
} cos_error_code_e;
```

## Server Exceptions

When the code member value in the cos_status_t structure is above 0, a network error has occurred.

The cos_status_t structure is described as follows:

<table>
   <tr>
      <th nowrap="nowrap">cos_status_t Member</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>code</td>
      <td>Status code in the response. 4xx indicates that the request failed due to a client exception; while 5xx indicates that the request failed due to a server exception. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730)</td>
      <td>Int</td>
   </tr>
   <tr>
      <td>error_code</td>
      <td>Error code returned by the body when the request fails. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730)</td>
      <td>String</td>
   </tr>
   <tr>
      <td>error_msg</td>
      <td>Error message returned by the body when the request fails. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730)</td>
      <td>String</td>
   </tr>
   <tr>
      <td>req_id</td>
      <td>Request ID used to uniquely identify the request</td>
      <td>String</td>
   </tr>
</table>
