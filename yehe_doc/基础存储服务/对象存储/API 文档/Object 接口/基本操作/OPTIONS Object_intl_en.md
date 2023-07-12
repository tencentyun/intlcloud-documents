## Overview

This API is used to issue a preflight request for cross-origin resource sharing (CORS). Before an actual CORS request is sent, your browser may determine whether a preflight request is necessary and if yes, it automatically issues a preflight request first. Therefore, frontend developers may not need to send such requests themselves in most cases.
- If the preflight request matches the CORS configuration of the bucket, COS will respond successfully, allowing the browser to send the actual CORS request.
- If the bucket does not have CORS configuration, or the preflight request does not match the configuration, COS returns the 403 Forbidden error, and the browser will stop the CORS request and throw an exception to the frontend.
- For more information about CORS configurations, please see [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279).


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=OptionsObject&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>

## Request

#### Sample request

```plaintext
OPTIONS /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Origin: Origin
Access-Control-Request-Method: RequestMethod
```

>!
>- In the sample request above, an object key (`ObjectKey`) is specified. You can also specify any other resources in the bucket, such as `OPTIONS / HTTP/1.1` or `OPTIONS /?lifecycle HTTP/1.1`.
>- As the preflight request is automatically sent by your browser, you cannot and need not include a request signature.
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> 

#### Request parameters

The request parameters are determined by the browser based on the target cross-origin resource.

#### Request headers

The request headers are determined by the browser based on the target cross-origin resource.

| Header | Description | Type | Required |
| --- | --- | --- | --- |
| Origin | Domain that initiates the CORS request | string | Yes |
| Access-Control-Request-Method | Method used for the CORS request | string | Yes |
| Access-Control-Request-Headers | HTTP request headers used for the CORS request. You can use commas (,) to separate multiple headers (case-insensitive). | string | No |

#### Request body

This API does not have a request body.

## Response

#### Response headers

The browser automatically identifies the response headers and controls whether the CORS request is allowed.

| Header | Description | Type |
| --- | --- | --- |
| Access-Control-Allow-Origin | Domains that are allowed to send a CORS request. Valid values: <br><li>`*`: all domains<br><li>Domains specified in the `Origin` request header | string |
| Access-Control-Allow-Methods | Methods allowed for the CORS request. Multiple methods are separated by commas (,). | string |
| Access-Control-Expose-Headers | HTTP response headers (case-insensitive) of CORS requests that the browser can get. Multiple headers are separated by commas (,). | string |
| Access-Control-Max-Age | Validity period of the CORS configuration, in seconds. Within the validity period, the browser does not need to issue a preflight request again for the same request. | integer |

#### Response body

The response body of this API is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

The following sample preflight requests are all automatically issued by the browser according to the actual CORS requests.

#### Example 1: initiating a preflight request for `PUT Object`

#### Request

```plaintext
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 14:49:22 GMT
Origin: https://example.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: content-md5,content-type,x-cos-meta-author
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: content-md5,content-type,x-cos-meta-author
Access-Control-Allow-Methods: PUT,GET,POST,DELETE,HEAD
Access-Control-Allow-Origin: https://example.com
Access-Control-Expose-Headers: Content-Length,ETag,x-cos-meta-author
Access-Control-Max-Age: 600
Date: Thu, 09 Jul 2020 14:49:22 GMT
Server: tencent-cos
x-cos-request-id: NWYwNzJlNzJfODRjOTJhMDlfMjU0MWNfMTNmZDM5****
```

#### Example 2: initiating a preflight request when `GET Object` carries the `range` request header

#### Request

```plaintext
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 14:49:22 GMT
Origin: https://example.com
Access-Control-Request-Method: GET
Access-Control-Request-Headers: range
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Access-Control-Allow-Headers: range,x-cos-server-side-encryption-customer-algorithm,x-cos-server-side-encryption-customer-key,x-cos-server-side-encryption-customer-key-md5
Access-Control-Allow-Methods: GET,HEAD
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: Content-Length,ETag,x-cos-meta-author
Access-Control-Max-Age: 600
Date: Thu, 09 Jul 2020 14:49:22 GMT
Server: tencent-cos
x-cos-request-id: NWYwNzJlNzJfZDUyNzVkNjRfYTA2Ml8yNGEz****
```

#### Example 3: initiating a preflight request for `PUT Bucket lifecycle`

#### Request

```plaintext
OPTIONS /?lifecycle HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 14:29:40 GMT
Origin: https://bar.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: content-md5,content-type
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: close
Access-Control-Allow-Credentials: true
Access-Control-Allow-Headers: content-md5,content-type
Access-Control-Allow-Methods: PUT,GET,POST,DELETE,HEAD
Access-Control-Allow-Origin: https://bar.com
Access-Control-Expose-Headers: Content-Length,ETag,x-cos-meta-author
Access-Control-Max-Age: 600
Date: Thu, 09 Jul 2020 14:29:40 GMT
Server: tencent-cos
x-cos-request-id: NWYwNzI5ZDRfNjFiMDJhMDlfYzk2NF8xYmZl****
```

#### Example 4: bucket with no CORS configuration, or preflight request not matching the CORS configuration

#### Request

```plaintext
OPTIONS /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Thu, 09 Jul 2020 11:45:26 GMT
Origin: https://example.com
Access-Control-Request-Method: PUT
Connection: close
```

#### Response

```plaintext
HTTP/1.1 403 Forbidden
Content-Type: application/xml
Content-Length: 687
Connection: close
Date: Thu, 09 Jul 2020 11:45:26 GMT
Server: tencent-cos
x-cos-request-id: NWYwNzAzNTZfNzNjODJhMDlfMzRiM2ZfMThjMjk4****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OWE4OGMxZjNjY2JiNTBmMTVmMWY1MzAzYzkyZGQ2ZWM4OWM4Y2M5MzI5ZmUzN2FjZDk1OTRjYWI5Yjg5OTJlZDA=

<?xml version='1.0' encoding='utf-8' ?>
<Error>
	<Code>AccessForbidden</Code>
	<Message>CORSResponse: This CORS request is not allowed. This is usually because the evalution of Origin, request method / Access-Control-Request-Method or Access-Control-Requet-Headers are not whitelisted by the resource&apos;s CORS spec</Message>
	<Resource>examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject</Resource>
	<RequestId>NWYwNzAzNTZfNzNjODJhMDlfMzRiM2ZfMThjMjk4****</RequestId>
	<TraceId>OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OWE4OGMxZjNjY2JiNTBmMTVmMWY1MzAzYzkyZGQ2ZWM4OWM4Y2M5MzI5ZmUzN2FjZDk1OTRjYWI5Yjg5OTJlZDA=</TraceId>
</Error>
```
