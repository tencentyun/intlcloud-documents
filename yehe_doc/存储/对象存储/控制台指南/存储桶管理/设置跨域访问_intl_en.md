## Overview

You can set cross-origin resource sharing (CORS) for objects in buckets in the COS console. COS supports configuring multiple rules to respond to OPTIONS requests. CORS is to request resources over HTTP from an origin for another origin. Two origins that differ in protocol, domain name, or port are treated as different origins.

COS can respond to CORS OPTIONS requests and return specified rules to the browser as configured by you, but the server does not verify whether subsequent cross-origin requests conform to the rules. For more information, see [Cross-Origin Resource Sharing (CORS)](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS) and [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/11488).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Find the target bucket and click the bucket name to enter the bucket details page.
4. Select **Security Management** > **CORS (Cross-Origin Resource Sharing)** on the left sidebar and click **Add a Rule**.
![](https://main.qcloudimg.com/raw/1659089c942ec8fadd77c880f1d4f492.png)
5. Add rule information (fields marked with * are required). Configuration items are as follows:
![](https://main.qcloudimg.com/raw/6a1f4bed7f42fba69449514822759c42.png)
 - **Origin**: The sources from which cross-origin requests are allowed. You can add domain names and IP addresses.
    - The domain name does not need to end with a slash (`/`).
    - Multiple domain names can be specified, with one domain name per line.
    - Asterisk (*) is supported, meaning that all domain names and IP addresses are allowed. This is not recommended.
    - A single specific domain name such as `http://www.abc.com` is supported.
    - Second-level wildcard domain names such as `http://*.abc.com` are supported. Note that each line can contain only one `*`.
    - Do not omit the protocol name HTTP or HTTPS. If the port is not the default port 80, the port should also be specified. An sample IP address is `http://10.10.10.10`.
 - **Allow-Methods**: GET, PUT, POST, DELETE, and HEAD methods are supported. You can enumerate one or more allowed cross-origin request methods.
 - **Allow-Headers**: This parameter informs the server what custom HTTP headers (such as x-cos-meta-md5) are allowed in subsequent requests through an OPTIONS request.
    - Multiple headers can be specified, with one header per line, such as `Content-type`.
    - Headers may be easily omitted. Therefore, if there is no special requirement, we recommend you set this field to `*`, meaning that all headers are allowed.
    - Uppercase and lowercase letters [a-z,A-Z] are supported, while underscore (_) is not.
    - Each header specified in `Access-Control-Request-Headers` must correspond to a value in `Allow-Headers`.
 - **Expose-Headers**: Headers commonly used by COS. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728). Set this parameter based on your specific application requirements. `ETag` is recommended. Wildcard is not allowed. The headers are case-insensitive, with one header per line.
 - **Max-Age**: Validity period of the result obtained by `OPTIONS` in seconds. The value must be a positive integer, such as 600.
 - **Return Vary: Origin**: Set whether to return the `Vary: Origin` header. Enable this option if the browser has both CORS and non-CORS requests; otherwise, cross-origin access issues will occur.
 >! If `Vary: Origin` is selected, browser access or CDN origin-pull requests may increase.
6. After configuration, click **Submit** and you will see the CORS rule added. To modify it, click **Edit**.
![](https://main.qcloudimg.com/raw/c4399193611b4f81e57a549634ea865a.png)
