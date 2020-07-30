## API Description

This API is used to initiate a preflight request for cross-origin resource sharing (CORS). Your browser may automatically send such a request before a real CORS request if it determines that it’s necessary to do so. Therefore, frontend developers normally need not call this API manually.
- If the specified bucket has a CORS configuration which the preflight request matches, COS returns a success response, allowing the browser to continue the CORS request.
- If the specified bucket has no CORS configuration or the preflight request does not match the bucket's CORS configuration, COS returns HTTP 403 Forbidden, and the browser stops the CORS request and throws an exception to the front end instead.
- For information about bucket CORS configuration, see [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279).

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
>- Although the above example uses ObjectKey, a preflight request can actually be initiated for any resource (including root directory) under a bucket endpoint, such as `OPTIONS / HTTP/1.1` or `OPTIONS /?lifecycle HTTP/1.1`.
>- The preflight request is automatically sent by your browser, so you cannot and need not include an authorization request signature in the request.

#### Request parameters

The request parameters of this API are automatically determined by the browser based on the destination resource for cross-origin access.

#### Request headers

The request headers of this API are automatically determined by the browser based on the cross-origin access action.

| Name | Description | Type | Required |
| --- | --- | --- | --- |
| Origin | Domain name from which a CORS request is initiated. | string | Yes |
| Access-Control-Request-Method | The method used for initiating a CORS request | string | Yes |
| Access-Control-Request-Headers | HTTP request headers used for initiating a CORS request. Case-insensitive; separated with a comma (,) | string | No |

#### Request body

This API does not have a request body.

## Response

#### Response headers

The response headers of this API are automatically returned by the browser as it identifies, processes and allows a CORS request.

| Name | Description | Type |
| --- | --- | --- |
| Access-Control-Allow-Origin | Domain name from which a CORS request is allowed. Valid values: <br><li>`*`: allows all domain names<br><li>Domain names specified in the `Origin` request header: allow only the specified domain names | string |
| Access-Control-Allow-Methods | Methods allowed for initiating a CORS request and separated with a comma (,) | string |
| Access-Control-Expose-Headers | HTTP response headers that the browser is allowed to return for a CORS request. Case-insensitive; separated with a comma (,) | string |
| Access-Control-Max-Age | Validity duration in sec of a CORS configuration. Within the duration, the browser need not initiate a preflight request again for the same request | integer |

#### Response body

The response body of this API is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

In the following examples, preflight requests are all automatically initiated by the browser based on real CORS requests.

#### Example 1. Initiate a preflight request for PUT Object

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

#### Example 2. Initiate a preflight request for GET Object with specified Range request header

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

#### Example 3. Initiate a preflight request for PUT Bucket lifecycle

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

#### Example 4. The specified bucket has no CORS configuration, or the preflight request does not match the CORS configuration

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
