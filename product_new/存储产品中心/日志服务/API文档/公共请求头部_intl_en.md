## Overview

This document describes common request headers that need to be included when CLS APIs are used. The following headers will not be detailed in specific API documents.

## Common Request Header List

| HTTP Header Name | Description                                        |
| ------------------- | ------------------------------------------------------------ |
| Host                | Request host name, which varies by region, such as `ap-shanghai.cls.tencentyun.com` for the Shanghai region |
| Authorization       | Signing information. For the calculation method, please see [Request Signature](https://intl.cloud.tencent.com/document/product/614/12445) |
| Content-Length      | Request body length. If there is no body, this header can be optional              |
| Content-Type        | Request body format. If there is no body, this header can be optional. It is determined by the specific API document. Currently, `application/json` and `application/x-protobuf` are supported |
| Content-MD5         | MD5 value of request body. If there is no body, this header can be optional. The calculation result is in lower case |
| x-cls-compress-type | Compression method used by requested body. Currently, lz4 compression is supported. This header is required only by the log upload API. If no compression is performed, it can be optional |

