## Configuration Overview

When an user requests your service resource, you can add a custom header in the **response message** to implement cross-origin resource sharing.
Response header is configured at the domain name level, therefore, once the configuration takes effect, it will be applied to the responses of all resources under the domain name. Response header configuration only makes changes to the client (browser) response but not to the CDN node cache.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to find the **Response Header Settings** section. It is disabled by default. You can click **Add Rule** to add response header rules.
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Operation

| Operation | Description                                                         |
| -------- | ------------------------------------------------------------ |
| Change     | Changes the specified response header parameter value.<br/>If there are duplicate header parameters, they will all be changed and merged into one header.<br/>If the target header does not exist, a new one will be created.|
| Add     | Adds the specified response header parameter.<br/>Parameters can be duplicate. <br/>You can add parameters with the same name and different values (x-cdn:value1,x-cdn:value2) and even parameters with the same name and value (x-cdn:value1,x-cdn:value1). <br/>**Note: Adding headers may affect the request. It’s recommended to change the header instead of adding one.** |
| Delete     | Deletes the specified response header parameter.                                       |

> !
> - Some headers cannot be added, deleted, or changed by yourself. For the detailed list, please see [Note](#notice).
> - You can configure up to 10 response header rules and adjust their priorities. Rules at the bottom of the list have higher priorities.

### Header parameter

<table>
<thead>
<tr>
<th style="width:230px">Header Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Access-Control-Allow-Origin</td>
<td>It specifies which domains can access the resource. Up to 10 domains can be configured. For the request whose host is added to this list, the corresponding value will be filled in to the response header. You can also set it as `*` to allow all domains to access resources. For more information, please see <a href="#acao">Access-Control-Allow-Origin Match Mode Introduction</a>.<br>You can enter wildcard `*`, domain names, and IPs. `http://` or `https://` must be contained (E.g., `http://test.com,http://1.1.1.1`). Please separate multiple ones with `,`, and up to 66 entries are supported. </td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Specifies the cross-origin HTTP request method and supports multiple methods at the same time.<br>Valid values: `POST`, `GET`, and `OPTIONS`.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Specifies the validity period (in seconds) of a preflight request.<br>For a non-simple cross-origin request, it needs to add an HTTP query request, (namely the preflight request) before the communication to check whether the cross-origin request is trusted. The following requests are considered as non-simple cross-origin requests: <br>1) Requests whose method is not GET, HEAD, or POST; <br>2) POST requests whose request data type is not `application / x-www-form-urlencoded`, `multipart / form-data` or `text / plain` (for example `application/xml` and `text/xml`)<br>For example, if the custom request header is `Access-Control-Max-Age:1728000`, it indicates that there will not be another preflight request sent for the cross-origin access to the resource within 1,728,000 seconds (20 days).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Specifies which headers can be exposed to clients as a part of response.<br>By default, these 6 headers can be exposed to clients: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, and `Pragma`.<br>If you want to make other headers accessible to clients, you can separate multiple headers with `,`, e.g., `Access-Control-Expose-Headers: Content-Length,X-My-Header`. In this way, clients can access the two headers `Content-Length` and `X-My-Header`.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Activates download in the browser and sets the default filename of the downloaded resource.<br>When a server sends a file to a client browser, if the file type is supported by the browser, such as TXT and JPG, the file will be directly opened in the browser by default. If you want the user to save the file, you can configure the `Content-Disposition` field to override the browser's default behavior. The common configuration is as follows:<br>`Content-Disposition:attachment;filename=FileName.txt`</td>
</tr>
<tr>
<td>Content-Language</td>
<td>Specifies the language code used on the page. The common configuration is as follows:<br>`Content-Language: en-US`</td>
</tr>
<tr>
<td>Custom</td>
<td>Supports custom header parameters in key-value format.<br>Parameter key: 1 to 100 characters, supporting uppercase and lowercase letters, digits, and hyphens (-).<br>Parameter value: 1 to 1000 characters</td>
</tr>
</tbody></table>


### Access-Control-Allow-Origin match mode introduction[](id:acao)

| **Match Mode**   | **Origin Value**                                                     | **Description**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| All         | *                                                            | If it is set to `*`, the header `Access-Control-Allow-Origin:*` is added to all responses. |
| Full match       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` |For requests from `https://cloud.tencent.com`, the response header is `Access-Control-Allow-Origin: https://cloud.tencent.com`. If the request is from `https://www.qq.com`, which is not specified in the rule, the response will not change. |
| Second-level wildcard domain name match | `http://*.tencent.com`                                       | For requests from `https://cloud.tencent.com`, the header `Access-Control-Allow-Origin: https://cloud.tencent.com` will be added to the response. If the request is from `https://cloud.qq.com`, which is not specified in the rule, so the response will not change. |
| Port match       | `https://cloud.tencent.com:8080`                             | For requests from `https://cloud.tencent.com:8080`, the header `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` will be added to the response. The source `https://cloud.tencent.com` does not hit the list, so the response will not change. |

> ! In Port Match mode, you must specify the port.

[](id:notice)
### Note

The following headers currently cannot be added, deleted, or changed.

```
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
