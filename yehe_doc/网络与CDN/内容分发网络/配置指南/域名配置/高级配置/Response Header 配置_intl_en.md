## Configuration Overview

When an end user requests a business resource, you can add a custom header in the returned **response message** to implement cross-origin resource sharing.
The response header is configured at the domain name level. Once the configuration takes effect, it will be synced to the response message of each resource under the domain name. Response header configuration only makes changes to the client (browser) response but not to the CDN node cache.

## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to see the **Response Header Configuration** section. It is disabled by default. You can click **Add Rule** to add response header rules.
![img](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Operation

| Operation | Description                                                         |
| :------- | :----------------------------------------------------------- |
| Set     | Changes the value of a specified response header parameter.<br/>If the target header does not exist, it will be added after the change.<br/>If the header parameter already exists, all the duplicates will be changed and merged into one header. For example, after the rule "Set - `x-cdn: value1`" is configured, if a request contains multiple `x-cdn` headers, the headers will be changed and merged into one header `x-cdn: value1`. |
| Delete     | Deletes a specified response header parameter.                                       |

> !
> - Some headers cannot be set or deleted in a self-service manner. For the detailed list, please see [Notes](#notice).
> - Up to 10 response header rules can be configured.
> - Rule priority can be adjusted. Rules lower on the list have higher priority. If a header parameter is configured with multiple rules, the bottom rule will take effect as rules are executed from bottom to top.

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
<td>Cross-origin permission-related header, which specifies the domain allowed to access resources. Up to 10 domains can be configured. If a source request host is configured as a header parameter value, it will be filled in to the response header. You can also set it as `*` to allow all domains to access resources. For more information, please see <a href="#acao">Access-Control-Allow-Origin Match Mode Description</a>.<br>The wildcard `*`, domain names, and IPs are supported. `http://` or `https://` must be contained. Please separate multiple ones with `,`, and up to 66 entries are supported. E.g., `http://test.com,http://1.1.1.1`. </td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Specifies the cross-origin HTTP request method and supports multiple methods at the same time: <br>`Access-Control-Allow-Methods: <code>POST, GET, OPTIONS`</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Specifies the validity period (in seconds) of a preflight request.<br>For a non-simple cross-origin request, an HTTP query request, namely the preflight request, is needed before the official communication to check whether the cross-origin request is secure to be accepted. A cross-origin request is non-simple if it is:<br>Not a GET, HEAD, or POST request, or it is a POST request but its request data type is `application/xml`, `text/xml`, or any other data type except `application/x-www-form-urlencoded`, `multipart/form-data`, and `text/plain`.<br>For example, if a custom request header is `Access-Control-Max-Age:1728000`, it indicates that there will not be another preflight request sent for the cross-origin resource sharing within 1,728,000 seconds (20 days).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Specifies which headers can be exposed to clients as a part of responses.<br>By default, these 6 headers can be exposed to clients: `Cache-Control`, `Content-Language`, `Content-Type`, `Expires`, `Last-Modified`, and `Pragma`.<br>If you want to make other headers accessible to clients, you can separate multiple headers with `,`, e.g., `Access-Control-Expose-Headers: Content-Length,X-My-Header`. In this way, clients can access the two headers `Content-Length` and `X-My-Header`.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Activates download in the browser and sets the default filename of the downloaded resource.<br>When a server sends a file to a client browser, if the file type is supported by the browser, such as TXT and JPG, the file will be directly opened in the browser by default. If you want the user to save the file, you can configure the `Content-Disposition` field to override the browser's default behavior. The common configuration is as follows:<br>`Content-Disposition:attachment;filename=FileName.txt`</td>
</tr>
<tr>
<td>Content-Language</td>
<td>Specifies the language code used on the page. The common configuration is as follows:<br>`Content-Language: zh-CN`<br>`Content-Language: en-US`</td>
</tr>
<tr>
<td>Custom</td>
<td>Supports custom header and key-value pair settings.<br>Requirements on custom header parameters: consisting of 1 to 100 characters of uppercase and lowercase letters, digits, and hyphens (-).<br>Requirements on custom header values: consisting of 1 to 1000 characters; Chinese characters are not supported.</td>
</tr>
</tbody></table>

[](id:acao)
### Access-Control-Allow-Origin match mode introduction

| **Match Mode**   | **Origin Value**                                                     | **Description**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Full match         | *                                                            | If it is set to `*`, the header `Access-Control-Allow-Origin:*` will be added to the response. |
| Fixed match       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | The source `https://cloud.tencent.com` hits the list, so the header `Access-Control-Allow-Origin: https://cloud.tencent.com` will be added to the response. The source `https://www.qq.com` does not hit the list, so the response will not change. |
| Second-level wildcard domain name match | `http://*.tencent.com`                                       | The source `https://cloud.tencent.com` hits the list, so the header `Access-Control-Allow-Origin: https://cloud.tencent.com` will be added to the response. The source `https://cloud.qq.com` does not hit the list, so the response will not change. |
| Port match       | `https://cloud.tencent.com:8080`                             | The source `https://cloud.tencent.com:8080` hits the list, so the header `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` will be added to the response. The source `https://cloud.tencent.com` does not hit the list, so the response will not change. |

> ! If there are special ports, you need to enter the relevant information in the list. Arbitrary port match is not supported, and you must specify the ports.

[](id:notice)
### Notes

The headers below are not supported and will not take effect even if configured:

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
