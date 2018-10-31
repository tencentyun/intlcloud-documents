## Description

This document describes the common request headers to be used when using APIs.

### Request Headers

| Header Name | Description | Type | Required |
| ---------------------- | ---------------------------------------- | ------ | ---- |
| Authorization | The header required for the request signature. | string | Yes |
| Content-Length | Length of request content. It is required for archive upload. | string | No    |
| Host | Specifies the service endpoint to which the request is sent. For more information on supported regions, see [Regions](/document/product/572/8727#.E5.9C.B0.E5.9F.9F---region) | string | Yes |
| x-cas-content-sha256 | The SHA256 checksum of the archive or archive chunk to be uploaded. For the content of 1 MB, the value of this header is the same as that of x-cas-sha256-tree-hash, although they are calculated by different methods.<br /> It is required for archive or archive chunk upload. | string | No    |
| x-cas-sha256-tree-hash | The SHA256 tree-hash checksum of the archive or archive chunk to be uploaded. <br />It is required for archive or archive chunk upload. | string | No    |

