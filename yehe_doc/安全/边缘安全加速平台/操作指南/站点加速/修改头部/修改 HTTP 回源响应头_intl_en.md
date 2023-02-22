## Overview
You can customize, add, and delete headers in HTTP responses from nodes to clients, which will not affect the node cache.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create rules to modify HTTP response headers as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Description of configuration items:
<table>
<thead>
<tr>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Set</td>
<td>Sets the specified header to the specified value. The header must be unique.<br>Note: If the specified header does not exist, it will be added.</td>
</tr>
<tr>
<td>Add</td>
<td>Adds the specified header.<br>Note: If the header already exists, it will be overwritten for uniqueness.</td>
</tr>
<tr>
<td>Delete</td>
<td>Deletes the specified header.</td>
</tr>
</tbody></table>

## Notes
- A custom header parameter must be in the following format:
  - Parameter name: It can contain 1–100 digits, letters, and hyphens.
  - Parameter value: It can contain 1–1000 characters.
- During one HTTP request header modification operation, you can add up to 30 headers of different types, which will be executed in sequence from top to bottom.
- The following standard headers cannot be modified:

```js.
Date
Expires
Content-Type
Content-Encoding
Content-Length
Transfer-Encoding
Cache-Control
If-Modified-Since
Last-Modified
Connection
Content-Range
ETag
Accept-Ranges
Age
Authentication-Info
Proxy-Authenticate
Retry-After
Set-Cookie
Vary
WWW-Authenticate
Content-Location
Content-MD5
Content-Range
Meter
Allow
Error
```

## Configuration Samples
### Access-Control-Allow-Origin
This header requests permission to access cross-origin resources, so as to implement CORS.

- Header name: Access-Control-Allow-Origin.
- Header value: Enter domain names and/or IPs starting with "http://"/"https://", separated by commas (up to 1000 characters). Note that wildcards (*) can be used. Example: `http://test.com,http://1.1.1.1`.
- Value description:
<table>
<thead>
<tr>
<th width="20%">Header value</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>*</td>
<td>Matches all origins: <br>The header <code>Access-Control-Allow-Origin:*</code> is included in the response to allow requests from all origins.</td>
</tr>
<tr>
<td><code>http://intl.cloud.tencent.com</code>, <code>https://intl.cloud.tencent.com</code>,<code>http://www.b.com</code></td>
<td>Matches specific origins: <ul><li>The origin <code>https://intl.cloud.tencent.com</code> hits the list of allowed origins, so the header <code>Access-Control-Allow-Origin: https://intl.cloud.tencent.com</code> is included in the response. </li><li>The origin <code>https://www.qq.com</code> doesn't hit the list, so the Access-Control-Allow-Origin header is not present.</li></td>
</tr>
<tr>
<td><code>https://*.tencent.com</code></td>
<td>Matches origins by second-level wildcard domain name: <ul><li>The origin <code>https://intl.cloud.tencent.com</code> hits the list of allowed origins, so the header <code>Access-Control-Allow-Origin: https://intl.cloud.tencent.com</code> is included in the response.</li><li>The origin <code>https://cloud.qq.com</code> doesn't hit the list, so the Access-Control-Allow-Origin header is not present.</li></td>
</tr>
<tr>
<td><code>https://cloud.tencent.com:8080</code></td>
<td>Matches origins by port: <ul><li>The origin <code>https://cloud.tencent.com:8080</code> hits the list of allowed origins, so the header <code>Access-Control-Allow-Origin:https://cloud.tencent.com:8080</code> is included in the response.</li><li>The origin <code>https://intl.cloud.tencent.com</code> doesn't hit the list, so the Access-Control-Allow-Origin header is not present.</li>Note: A special port used by the origin must be added to the header value.</td>
</tr>
</tbody></table>

### Access-Control-Expose-Headers
This header specifies headers that can be exposed as part of the response.
>? By default, the following six headers can be exposed to the client: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, and `Pragma`.

- Header name: Access-Control-Expose-Headers.
- Header value: Enter header names to be exposed to the client except the six default headers and separate them by semicolon, such as `Content-Length`,`X-My-Header`.

### Content-Disposition
This header activates download in the browser and sets the default name of the downloaded file.

When the server sends a file supported by the client browser (such as a TXT or JPG file), the browser opens the file by default. If you want to ask the user to save the file, configure the `Content-Disposition` field to override the browser's default behavior.

- Header name: Content-Disposition.
- Header value: `attachment;filename=FileName.txt`.

### Access-Control-Allow-Methods
This header specifies the HTTP request methods allowed for cross-origin access.

- Header name: Access-Control-Allow-Methods.
- Header value: Multiple values can be set, such as `POST`, `GET`, and `POTIONS`.


### Access-Control-Max-Age
This header specifies the validity period of the result of a preflight request in seconds.
>? A non-simple CORS request requires a preflight request (that uses HTTP request methods) before being initiated. It is made to check whether the CORS request is secure and acceptable. Typical cases requiring preflight requests:
A CORS request uses methods other than `GET`, `HEAD`, and `POST` or is initiated via `POST` with the request data type other than `application / x-www-form-urlencoded`, `multipart / form-data`, and `text / plain` (such as `application / xml` or `text / xml`).

- Header name: Access-Control-Max-Age.
- Header value: Enter the number of seconds, for example, `1728000`.


### Content-Language
This header specifies the language to be used by the accessed page.
- Header name: Content-Language.
- Header value: `zh-CN` or `en-US`.
