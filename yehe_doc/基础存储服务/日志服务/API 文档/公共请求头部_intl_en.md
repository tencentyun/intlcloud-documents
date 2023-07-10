## Overview

This document describes common request headers that will be used in CLS API requests. The headers mentioned below will not be described again in related API documentation.

## List of Common Request Headers

| HTTP Header | Description |
| ------------------- | ------------------------------------------------------------ |
| Host                | Domain name, which differs by region. For example, the value for Shanghai is `ap-shanghai.cls.tencentyun.com`. For details, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940). |
| Authorization | Signature content. For details on how to calculate it, see [Request Signature](https://intl.cloud.tencent.com/document/product/614/12445). |
| Content-Length | Length of the request body. If there is no request body, this header can be ignored. |
| Content-Type | Format of the request body. Valid values: `application/json`, `application/x-protobuf`. You can select the value according to the corresponding API documentation. If there is no request body, this header can be ignored. |
| Content-MD5 | MD5 value of the request body, which is expressed in lowercase letters. If there is no request body, this header can be ignored. |
| x-cls-compress-type | The compression method (LZ4) for the request body, which is used only by log upload APIs. If the request body is not compressed, this header can be ignored. |
| x-cls-token | Temporary key credential, which is the key token returned for an STS request. This header is required when CLS is accessed via temporary keys. |

