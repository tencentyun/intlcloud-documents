## Overview

This section describes common request headers when using CLS APIs. The headers below will not be described again in API documents.

## List of Common Request Headers

| HTTP Header Name | Description |
| ------------------- | ------------------------------------------------------------ |
| Host | Hostname of the request, which is different for each region. For example, it is ap-shanghai.cls.myqcloud.com for Shanghai. |
| Authorization | Signature content. For more information on how to compute the signature, see [Request Signature](/document/product/614/12445). |
| Content-Length | Length of the request Body. If there is no Body, this header can be ignored. |
| Content-Type | Format of the request Body (application/json, application/x-protobuf), which can be selected according to the detailed API documentation. If there is no Body, this header can be ignored. |
| Content-MD5 | MD5 hashed value in the request Body. If there is no Body, this header can be ignored. The calculation result supports lowercase letters. |
| x-cls-compress-type | Compression method (lz4) used by the request Body, which is only used by the log upload API. If there is no compression, this header can be ignored. |


