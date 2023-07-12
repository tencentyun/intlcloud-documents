## Feature Description

This API (`HEAD Bucket`) is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, HTTP status code 200 will be returned.
- If you do not have permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=HeadBucket&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```plaintext
HEAD / HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

This API has no request parameter.

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This API does not have a request body.

## Response

#### Response headers

In addition to common response headers, this API also returns the following response headers. For more information about common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

| Name | Description | Type |
| -------------------- | ------------------------------------------------------------ | ---- |
| x-cos-bucket-az-type | AZ type of the bucket. This header is returned only for MAZ buckets. Fixed to `MAZ`. | Enum |
| x-cos-bucket-region | Bucket region, such as `ap-beijing`, `ap-hongkong`, and `eu-frankfurt`. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | Enum |

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: OAZ bucket

#### Request

```plaintext
HEAD / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Tue, 28 May 2019 03:16:12 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1559013372;1559020572&q-key-time=1559013372;1559020572&q-header-list=date;host&q-url-param-list=&q-signature=9085930afacf1e8a0ade2697b69353b27901****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: close
Date: Tue, 28 May 2019 03:16:12 GMT
Server: tencent-cos
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWNlY2E3ZmNfZjhjMDBiMDlfMTBjOWRfZDcz****
```

#### Sample 2: MAZ bucket

#### Request

```plaintext
HEAD / HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 04 Jun 2020 06:43:03 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1591252983;1591260183&q-key-time=1591252983;1591260183&q-header-list=date;host&q-url-param-list=&q-signature=aa996608fe79d122ed9667d9db3caa262ed6****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: close
Date: Thu, 04 Jun 2020 06:43:03 GMT
Server: tencent-cos
x-cos-bucket-az-type: MAZ
x-cos-bucket-region: ap-beijing
x-cos-request-id: NWVkODk3ZjdfZjI4NWQ2NF9hODhkXzRhNmQ0****
```
