## Overview

This API is used to delete the origin-pull configuration of a bucket.

## Request

#### Sample request

```plaintext
DELETE /?origin HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - This request should be used with a request body.



#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

The response body of this API is empty.


## Examples

#### Request

```plaintext
DELETE /?origin= HTTP/1.1
Host: examplebucket-1250000000.cos.ap-shanghai.myqcloud.com
Authorization: Auth String
Date: Sun, 28 Apr 2019 12:02:24 GMT
```

#### Response

```plaintext
HTTP/1.1 204 No Content 
Server: tencent-cos
Date: Mon, 28 Aug 2018 02:53:40 GMT
x-cos-request-id: NWNjNTk2NTFfMmM4OGY3MGFfNTI1****
```
