## Description
This document describes the common response headers returned during your use of APIs. 

## Response Headers

| Header | Description | Type |
| ---------------------- | ---------------------------------------- | ------ |
| Content-Length | The length of the response body (in bytes). | string |
| x-cas-requestId | The ID created by CAS to uniquely identify your request. In case of any problem during your use of CAS, you can use this value for troubleshooting. It is recommended to record these values. | string |
| x-cas-sha256-tree-hash | The SHA256 tree-hash checksum of the archive or inventory body. | string |

