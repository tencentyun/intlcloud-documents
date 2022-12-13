## Overview
You can change, add, and delete HTTP response headers (in responding to client users from nodes) without affecting node caching.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Rule engine** on the left sidebar.
2. On the **Rule engine** page, select the target site and modify HTTP response header rules as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).
Configuration item description:
<table>
<thead>
<tr>
<th>API Type</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Set</td>
<td>It changes the specified header parameter to the set value.<br>Note:<ul><li>If the specified header doesn't exist, it will be added.</li><li>If the header already exists (even if there are multiple duplicate headers), the original header will be overwritten, and multiple duplicate headers will be merged into one for uniqueness.</td>
</tr>
<tr>
<td>Add</td>
<td>It adds the specified header.<br>Note: <br>If the header already exists (even if there are multiple duplicate headers), the original header will be overwritten, and multiple duplicate headers will be merged into one for uniqueness.</td>
</tr>
<tr>
<td>Delete</td>
<td>It deletes the specified header.</td>
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

## Sample Configuration
### Access-Control-Allow-Origin
This header is used to solve the cross-origin permission problem of the resource, so as to implement cross-origin access.

- Header name: `Access-Control-Allow-Origin`.
- Header value: You can enter `*` or multiple domain names and/or IPs (they must contain `http://` or `https://`) and separate them by comma, such as `http://test.com,http://1.1.1.1`. This value can contain up to 1,000 characters.
- Value description:
<table>
<thead>
<tr>
<th width="20%">Header Value</th>
<th width="80%">Description</th>
</tr>
</thead>
<tbody><tr>
<td>*</td>
<td>Full match: <br>The header <code>Access-Control-Allow-Origin:*</code> is added to the response to allow requests from all origins.</td>
</tr>
<tr>
<td><code>http://intl.cloud.tencent.com</code>, <code>https://intl.cloud.tencent.com</code>,<code>http://www.b.com</code></td>
<td>Fixed match: <ul><li>The origin <code>https://intl.cloud.tencent.com</code> hits the list, so the following header will be added to the response: <code>Access-Control-Allow-Origin: https://intl.cloud.tencent.com</code>. </li><li>The origin <code>https://www.qq.com</code> doesn't hit the list, so the response will not change.</li></td>
</tr>
<tr>
<td><code>https://*.tencent.com</code></td>
<td>Second-level wildcard domain name match: <ul><li>The origin <code>https://intl.cloud.tencent.com</code> hits the list, so the following header will be added to the response: <code>Access-Control-Allow-Origin: https://intl.cloud.tencent.com</code>.</li><li>The origin <code>https://intl.cloud.qq.com</code> doesn't hit the list, so the response will not change.</li></td>
</tr>
<tr>
<td><code>https://cloud.tencent.com:8080</code></td>
<td>Port match: <ul><li>The origin <code>https://cloud.tencent.com:8080</code> hits the list, so the following header will be added to the response: <code>Access-Control-Allow-Origin:https://cloud.tencent.com:8080</code>.</li><li>The origin <code>https://intl.cloud.tencent.com</code> doesn't hit the list, so the response will not change.</li>Note: If there are special ports, you need to enter the relevant information in the list. Arbitrary port match is not supported, and you must specify the ports.</td>
</tr>
</tbody></table>

### Access-Control-Expose-Headers
This header indicates which headers can be exposed to clients as part of the response.
>? By default, the following six headers can be exposed to the client: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, and `Pragma`.

- Header name: `Access-Control-Expose-Headers`.
- Header value: Enter header names to be exposed to the client except the six default headers and separate them by semicolon, such as `Content-Length`,`X-My-Header`.

### Content-Disposition
This header activates download in the browser and sets the default name of the downloaded file.

When the server sends a file to the client browser, if it is in a type supported by the browser, such as TXT or JPG, it will be directly opened in the browser by default. If you want to ask the user to save the file, you can configure the `Content-Disposition` field to override the browser's default behavior.

- Header name: `Content-Disposition`.
- Header value: A common configuration is `attachment;filename=FileName.txt` for example.

### Access-Control-Allow-Methods
This header specifies the HTTP request methods allowed for cross-origin access.

- Header name: `Access-Control-Allow-Methods`.
- Header value: Multiple values can be set, such as `POST`, `GET`, and `POTIONS`.


### Access-Control-Max-Age
This header specifies the validity period of the result of a preflight request in seconds.
>? For a non-simple cross-origin request, before the formal communication, an HTTP query request called "preflight request" needs to be sent to check whether the cross-origin request is secure and acceptable. The following requests are considered as non-simple cross-origin requests:
The request is initiated in a method other than `GET`, `HEAD`, and `POST` or is initiated by using `POST` with a data type other than `application / x-www-form-urlencoded`, `multipart / form-data`, and `text / plain` (such as `application / xml` or `text / xml`).

- Header name: `Access-Control-Max-Age`.
- Header value: Enter the number of seconds, for example, `1728000`.


### Content-Language
This header specifies the language to be used by the accessed page.
- Header name: `Content-Language`.
- Header value: `zh-CN` or `en-US`.