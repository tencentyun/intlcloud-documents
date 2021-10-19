## Configuration Scenario
When an end user requests a business resource, you can add a custom header in the returned **response message** to implement cross-origin access.
As the HTTP header configuration is for a specified domain name, once the configuration takes effect, the configured header will be added to the response messages of user requests for any resource under this domain name. HTTP header configuration affects only response of the client (such as browser) rather than CDN node's caching behaviors.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click the domain name to enter its configuration page. You will find the response header configuration on the **Advanced Configuration** tab. It is disabled by default.
![](https://main.qcloudimg.com/raw/a1f9b4b00d788b58e2142cc98ca29ef9.png)

### Modifying the configuration
#### 1. Modify the configuration
Toggle the switch and add HTTP header configuration. Currently, the following headers can be configured. You can also add custom headers:
- Access-Control-Allow-Origin: it specifies the sources of cross-origin requests allowed to access the resource.
- Access-Control-Allow-Methods: it specifies the allowed methods of cross-origin requests.
- Access-Control-Max-Age: it specifies the validity period for caching the returned result of preflight request for a particular resource when a cross-origin request is initiated.
- Access-Control-Expose-Headers: it specifies the headers visible to the client when a cross-origin request is initiated.
- Content-Disposition: it activates download in the browser and sets the default filename of the downloaded file.
- Content-Language: it specifies the language code used by the webpage.
- Custom: you can add a custom header.

![](https://main.qcloudimg.com/raw/4f08e0ad6753bc7905c3244131513926.png)

**General configuration: Content-Disposition**
`Content-Disposition` is used to activate download in the browser and set the default filename of the downloaded resource. When the server sends a file to the client browser, if it is in a type supported by the browser, such as TXT or JPG, it will be directly opened in the browser by default. If you want to ask the user to save the file, you can configure the `Content-Disposition` field to override the browser's default behavior. The common configuration is as follows:
`Content-Disposition: attachment;filename=FileName.txt`

**General configuration: Content-Language**
`Content-Language` specifies the language code used by the webpage. Common configurations are as follows:
`Content-Language: zh-CN`
`Content-Language: en-US`

**Cross-origin configuration: Access-Control-Allow-Origin**
Cross-origin access refers to a scenario where a resource under a domain name, such as `www.abc.com`, initiates a request to another resource under another domain name, such as `www.def.com`. As the resource domain names are different, **cross-origin access** will occur. Using different protocols or ports can cause cross-origin access. You need to add configuration related to cross-origin access in the response header to make the first resource get the desired data.
- Feature overview:
`Access-Control-Allow-Origin` is used to solve the problem of cross-origin permissions of resources. Up to 10 values of origins allowed to access a resource can be configured. If a source request's host is in the configured domain name list, the corresponding value will be directly populated into the returned header. You can also set the wildcard "*" to allow all origins to access the resource.
- Match mode overview

| **Match Mode**   | **Origin Value**                                                     | **Description**                                                     |
| :------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Full match         | *                                                            | If it is set to "*", the following header will be added to the response: <br/>`Access-Control-Allow-Origin:*` |
| Fixed match       | `http://cloud.tencent.com`<br/> `https://cloud.tencent.com`<br/> `http://www.b.com` | The source `https://cloud.tencent.com` hits the list, so the following header will be added to the response: <br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>The source `https://www.qq.com` does not hit the list, so the response will not change. |
| Second-level wildcard domain name match | `http://*.tencent.com`                                       | The source `https://cloud.tencent.com` hits the list, so the following header will be added to the response: <br/>`Access-Control-Allow-Origin: https://cloud.tencent.com`<br/>The source `https://cloud.qq.com` does not hit the list, so the response will not change. |
| Port match       |`https://cloud.tencent.com:8080`                             | The source `https://cloud.tencent.com:8080` hits the list, so the following header will be added to the response: <br/>`Access-Control-Allow-Origin:https://cloud.tencent.com:8080`<br/>The source `https://cloud.tencent.com` does not hit the list, so the response will not change. |

>If there are special ports, you need to enter the relevant information in the list. Arbitrary port match is not supported, and you must specify the ports.

**Cross-origin configuration: Access-Control-Allow-Methods**

`Access-Control-Allow-Methods` is used to specify the HTTP request methods allowed for cross-origin access. Multiple methods can be set as follows:
Access-Control-Allow-Methods: `POST, GET, OPTIONS`

**Cross-origin configuration: Access-Control-Max-Age**
`Access-Control-Max-Age` specifies the validity period of a preflight request.
For a non-simple cross-origin request, before the formal communication, an HTTP query request called "preflight request" needs to be made to check whether the cross-origin request is secure and acceptable. The following requests are considered as non-simple cross-origin requests:
- The request is initiated in a method other than `GET`, `HEAD`, and `POST` or is initiated by using `POST` with a data type other than `application / x-www-form-urlencoded`, `multipart / form-data`, and `text / plain` (such as `application / xml` or `text / xml`).
- A custom request header is used.
`Access-Control-Max-Age` is measured in seconds. Below is a configuration sample:
Access-Control-Max-Age:`1728000`

This indicates that no more preflight requests will be sent for the cross-domain access to this resource within 1,728,000 seconds (20 days).

**Cross-origin configuration: Access-Control-Expose-Headers**
`Access-Control-Expose-Headers` specifies which headers can be exposed to the client as part of the response. By default, the following six types of headers can be exposed to the client:
- Cache-Control
- Content-Language
- Content-Type
- Expires
- Last-Modified
- Pragma

If you want the client to access other header information, you can use the following setting and separate multiple headers with ";".
`Access-Control-Expose-Headers: Content-Length,X-My-Header`
This indicates that the client can access `Content-Length` and `X-My-Header`.

**Custom header**
You can add a custom header and customize `key-value` settings:
![img](https://main.qcloudimg.com/raw/501fd6e92b1cecbdd8b444837470ceb3.png)
![img](https://main.qcloudimg.com/raw/66e85b5076895455b9c069e5967c423f.png)

Currently, the following headers cannot be added:
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
If multiple identical headers are added, the lower the position, the higher the priority, and the header below will overwrite the header above it.

#### 2. Disable the configuration
You can toggle the HTTP header switch to disable this feature. When the switch is off, existing configurations will not take effect in the production environment.
![](https://main.qcloudimg.com/raw/573effac1ca884f772f10da215410984.png)

>If your domain name is configured for global acceleration, the response header configuration will take effect globally. This configuration does not distinguish between requests from Mainland China and from outside Mainland China.
