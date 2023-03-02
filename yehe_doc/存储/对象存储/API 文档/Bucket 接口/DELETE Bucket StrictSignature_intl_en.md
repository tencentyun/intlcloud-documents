
## Overview

This API (`DELETE Bucket StrictSignature`) is used to delete the strict signature mode configuration of a bucket. In this mode, you can specify the request headers and parameters that must be signed for certain requests.

> !
>
> - When calling this API, make sure that you have the permission to manipulate the bucket's strict signature mode. The bucket owner has this permission by default. If you don't have it, request it from the owner. For the authorization process, see [COS Authorization and Identity Verification Process](https://intl.cloud.tencent.com/document/product/436/45228).


## Request

#### Sample request

```shell
DELETE /?strict-signature HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

>? 
>
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
>- Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

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

The response body returned is empty.
      

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

The following example deletes the strict signature mode configuration of the `examplebucket-1250000000` bucket:


```shell
DELETE /?strict-signature HTTP/1.1
Date: Date
Authorization: Auth String
Content-MD5: Content-MD5
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024
```

#### Response

After the request above is made, COS returns "204 No Content", indicating that the strict signature mode configuration has been successfully deleted for the bucket.

```shell
HTTP/1.1 204 No Content 
Server: tencent-cos
Date: Date
x-cos-id-2:0dfafa/DAPDIFdafdsfDdfSFFfdfKKJdafasiuKJK2
x-cos-request-id: NTlhM2I3M2JfMjQ4OGY3MGFfMWE1NF84****
```
