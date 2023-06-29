## Configuration Overview

When an end user requests a business resource, you can add a custom header in the returned **response message** to implement cross-origin resource sharing.
Response header configuration is of the domain name dimension, therefore, once the configuration takes effect, it will be synced to the response message of each resource under the domain name. Response header configuration only makes changes to the client (browser) response but not to the CDN node cache.

## Directions

### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Advanced Configuration** tab to find the **Response Header Configuration** setting, which is disabled by default. You can click **Add Rule** to add HTTP response header rules.
![](https://main.qcloudimg.com/raw/979a6f3254776cdadd5ca4dc71d631a6.png)

### Operation type

| Operation | Description                                                         |
| :------- | :----------------------------------------------------------- |
| Set     | Changes the value of a specified response header parameter.<br/>If the target header does not exist, it will be added after the change operation.<br>If the header parameter already exists, all the duplicates will be changed and merged into one header. For example, after the rule "Set - <code>x-cdn: value1</code>" is configured, if a request contains multiple <code>x-cdn</code> headers, the headers will be changed and merged into one header <code>x-cdn: value1</code>. |
| Delete     | Deletes a specified response header parameter.                                       |

> !
> - Some headers cannot be set or deleted in a self-service manner. For the detailed list, see [Notes](#noice).
> - Up to 10 HTTP response header rules can be configured.
> - Rule priority can be adjusted. Rules at the bottom of the list have higher priority. If a header parameter is configured with multiple rules, the bottom rule will take effect as rules are executed from bottom to top.

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
<td>Cross-origin resource sharing (CORS) header, which specifies the domain allowed to access resources. If a source request host is configured as a header parameter value, it will be filled in to the response header. You can also set it as <code>*</code> to allow all domains to access resources. For more information, see <a href="#acao">Access-Control-Allow-Origin Match Mode Description</a>.</br>The wildcard <code>*</code>, domain names, and IPs are supported. <code>http://</code> or <code>https://</code> must be contained. Please separate multiple ones with <code>,</code>, and up to 1000 characters are supported. E.g., <code>http://test.com,http://1.1.1.1</code>.</td>
</tr>
<tr>
<td>Access-Control-Allow-Methods</td>
<td>Specifies the CORS HTTP request method and supports multiple methods at the same time: <br>Access-Control-Allow-Methods: <code>POST, GET, OPTIONS</code>.</td>
</tr>
<tr>
<td>Access-Control-Max-Age</td>
<td>Specifies the validity period (in seconds) of a preflight request.<br>For a non-simple CORS request, an HTTP query request, namely the preflight request, is needed before the official communication to check whether the CORS request is secure to be accepted. A CORS request is non-simple if it is:<br>Not a GET, HEAD, or POST request, or it is a POST request but its request data type is <code>application/xml</code>, <code>text/xml</code> or any other data type except <code>application/x-www-form-urlencoded</code>, <code>multipart/form-data</code>, and <code>text/plain</code>.<br>For example, if a custom request header is <code>Access-Control-Max-Age:1728000</code>, there will not be another CORS preflight request sent within 1,728,000 seconds (20 days).</td>
</tr>
<tr>
<td>Access-Control-Expose-Headers</td>
<td>Specifies which headers can be exposed to clients as a part of responses.<br>By default, these 6 headers can be exposed to clients: <code>Cache-Control</code>, <code>Content-Language</code>, <code>Content-Type</code>, <code>Expires</code>, <code>Last-Modified</code>, and <code>Pragma</code>.<br>If you want to make other headers accessible to clients, you can separate multiple headers with <code>,</code>, e.g., <code>Access-Control-Expose-Headers: Content-Length,X-My-Header</code>. In this way, clients can access the two headers <code>Content-Length</code> and <code>X-My-Header</code>.</td>
</tr>
<tr>
<td>Content-Disposition</td>
<td>Activates download in the browser and sets the default filename of the downloaded resource.<br>When a server sends files to a client browser, with the file types such as TXT and JPG supported by the browser, the files will be directly opened in the browser by default. If you want the user to save the files, you can configure the <code>Content-Disposition</code> field to override the browser's default behavior. The common configuration is as follows:<br><code>Content-Disposition:attachment;filename=FileName.txt</code></td>
</tr>
<tr>
<td>Content-Language</td>
<td>Specifies the language code used on the page. The common configuration is as follows:<br><code>Content-Language: zh-CN</code><br><code>Content-Language: en-US</code></td>
</tr>
<tr>
<td>Custom</td>
<td>Supports custom header and key-value pair settings.<br>A custom header parameter supports 1-100 characters of uppercase and lowercase letters, digits, and hyphens (-).<br>The parameter value supports 1-1000 characters excluding Chinese characters.</td>
</tr>
</tbody></table>


### Access-Control-Allow-Origin match mode introduction[](id:acao)

| **Match Mode**   | **Origin Value**                                                     | **Description**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Full match         | *                                                            | If it is set to `*`, the header `Access-Control-Allow-Origin:*` will be added to the response. |
| Fixed match       | `http://cloud.tencent.com` `https://cloud.tencent.com` `http://www.b.com` | The source `https://cloud.tencent.com` hits the list, so the header `Access-Control-Allow-Origin: https://cloud.tencent.com` will be added to the response. <br/>The source `https://www.qq.com` does not hit the list, so the response will not change. |
| Second-level wildcard domain name match | `https://*.tencent.com`                                       | The source `https://cloud.tencent.com` hits the list, so the header `Access-Control-Allow-Origin: https://cloud.tencent.com` will be added to the response. <br/>The source `https://cloud.qq.com` does not hit the list, so the response will not change. |
| Port match       | `https://cloud.tencent.com:8080`                             | The source `https://cloud.tencent.com:8080` hits the list, so the header `Access-Control-Allow-Origin:https://cloud.tencent.com:8080` will be added to the response. <br/>The source `https://cloud.tencent.com` does not hit the list, so the response will not change. |

> ! If there are special ports, you need to enter the relevant information in the list. You must specify the port as arbitrary port match is not supported.

### Notes[](id:noice)

The headers below are not supported and will not take effect if configured:

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
